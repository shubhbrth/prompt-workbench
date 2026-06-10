---
name: mlops-workflow
description: Guides a 3-stage skill promotion model — dev, staging, production — for teams that need reproducible, versioned skill installs. Covers version pinning, project-scope sharing via git, skills-lock.json tracking, and rollback. Follows an evidence-backed approach without overclaiming any setup as universally optimal.
---

# MLOps Workflow for Skills

A 3-stage promotion model for skills used in team or production contexts. Treats skill installs with the same discipline as software dependencies: versioned, reproducible, and rollback-safe.

## When to Use This Skill

Use this skill when the user:

- Is installing skills for a team that shares a git repo
- Needs reproducible skill versions across machines or CI environments
- Wants to promote a skill from local testing to team use to production
- Is debugging inconsistent skill behavior across environments
- Needs to roll back a skill update

## The 3-Stage Promotion Model

| Stage | Goal | Install method | Pin? | Scope |
|-------|------|---------------|------|-------|
| **Dev** | Iterate fast, test locally | `npx skills add` or `--from-local` | No | User (`-g`) |
| **Staging** | Validate with team before promoting | `npx skills add owner/repo@tag` | Git tag | Project (committed to `.agents/skills/`) |
| **Production** | Locked, auditable, rollback-safe | `gh skill install --pin <sha>` | Commit SHA | Project (committed) |

Never promote directly from dev to production without a staging validation step.

## Stage 1: Development

Install the latest version for local iteration. No pinning required.

```bash
# Install latest via skills.sh (primary)
npx skills add <owner/repo@skill> -g -y

# Or install from a local directory during authoring
gh skill install ./my-skill-repo --from-local --agent claude-code
```

Update freely during development:

```bash
npx skills update
npx skills check
```

**Exit criteria for dev**: the skill works correctly on your machine for the target task.

## Stage 2: Staging

Pin to a release tag and share with the team via project-scope git commit.

```bash
# Pin to a specific tag (npx path)
npx skills add <owner/repo@v1.2.0>

# Or pin via gh CLI (project-scope, shared via git)
gh skill install <owner/repo> <skill-name> --pin v1.2.0 --agent claude-code --scope project
```

The project-scope install writes to `.agents/skills/` — commit this directory to share with the team.

```bash
git add .agents/skills/
git commit -m "chore: pin <skill-name> to v1.2.0 for staging validation"
```

Record the pinned version in `skills-lock.json` (see below).

**Exit criteria for staging**: at least one team member validates the skill on their machine using the pinned install.

## Stage 3: Production

Pin to a commit SHA for full reproducibility. SHA pins are immutable — a tag can be moved, a SHA cannot.

```bash
# Find the SHA for the tag
gh api repos/<owner>/<repo>/git/ref/tags/v1.2.0 --jq '.object.sha'

# Install pinned to SHA
gh skill install <owner/repo> <skill-name> --pin <sha> --agent claude-code --scope project

# Commit the locked install
git add .agents/skills/
git commit -m "chore: promote <skill-name> to production at <sha>"
```

Update `skills-lock.json` with the SHA.

**Exit criteria for production**: CI validates the pinned version loads correctly (see validate-skills workflow).

## skills-lock.json

Track all pinned skills in a `skills-lock.json` at the repo root, analogous to `package-lock.json`.

```json
{
  "skills": {
    "prechecks": {
      "source": "owner/prompt-workbench",
      "stage": "production",
      "pin": "abc1234def5678",
      "tag": "v1.0.0",
      "installed": "2026-06-10",
      "agent": "claude-code",
      "scope": "project"
    },
    "prompt-workbench": {
      "source": "owner/prompt-workbench",
      "stage": "staging",
      "pin": "v1.2.0",
      "installed": "2026-06-08",
      "agent": "claude-code",
      "scope": "project"
    }
  }
}
```

Commit `skills-lock.json` to git. Update it whenever a skill is promoted, updated, or rolled back.

## Rollback

If a promoted skill causes problems, roll back by re-pinning to the previous SHA.

```bash
# npx path — reinstall at a prior commit SHA
npx skills add owner/repo@<previous-sha>

# gh path
gh skill update owner/repo skill-name --pin <previous-sha>

# Restore the previous skills-lock.json entry and commit
git add skills-lock.json .agents/skills/
git commit -m "revert: roll back <skill-name> to <previous-sha>"
```

## Clarifying Questions to Ask Before Recommending a Stage

- Is this skill for personal use only, or shared with a team?
- Does the team have a shared git repo for agent skills?
- Is there a CI step that validates skill installs?
- Has this skill version been tested on the target machine/OS?
- Is there a documented rollback procedure if the skill breaks a workflow?

## Evidence Basis

- Version pinning rationale adapted from standard dependency management practices (npm lockfiles, pip freeze)
- `gh skill install --pin` behavior from https://cli.github.com/manual/gh_skill_install
- `.agents/skills/` project-scope behavior from gh skill install documentation
- SHA-over-tag recommendation: tags are mutable references in git; SHAs are immutable

Note: this workflow is a reasonable baseline, not a guarantee of correctness for every team setup. Adapt to your existing CI/CD practices.
