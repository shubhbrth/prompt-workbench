---
name: skill-audit
description: Audits all installed skills and produces a report flagging unpinned skills in production, sources with low install counts, skills with no tagged releases, and outdated skills. Output is suitable for a PR comment, CI step, or manual review. Does not modify any installs — read-only by default.
---

# Skill Audit

Audits installed skills and produces a structured report. Designed for teams that want to enforce production hygiene on their skill installs before merging or deploying.

## When to Use This Skill

Use this skill when the user:

- Wants a health check on all installed skills before a release
- Is preparing a PR that changes skill installs and wants a review summary
- Is setting up a CI step to enforce skill version discipline
- Suspects an installed skill is outdated or from an untrusted source
- Wants to identify which skills have no tagged releases (cannot be pinned)

## Audit Checks

Run the following checks for each installed skill. Report pass, warn, or fail per check.

### 1. Version Pin Status

| State | Label | Description |
|-------|-------|-------------|
| Pinned to SHA | PASS | Fully reproducible |
| Pinned to tag | WARN | Reproducible unless tag is moved |
| Unpinned (latest) | FAIL (in production) | Non-reproducible, breaks on updates |

**How to check**: inspect `skills-lock.json` or `.agents/skills/` metadata.

### 2. Install Count

```bash
npx skills find <skill-name>
```

Check the install count shown in results:

| Count | Label |
|-------|-------|
| 1K+ | PASS |
| 100–999 | WARN |
| < 100 | FAIL |
| Unknown | WARN |

### 3. Source Reputation

| Source | Label |
|--------|-------|
| `vercel-labs`, `anthropics`, `microsoft` | PASS |
| GitHub org with 1K+ stars | PASS |
| Unknown author with < 100 GitHub stars | FAIL |
| Private/internal source | INFO (not flagged) |

### 4. Tagged Releases

```bash
gh api repos/<owner>/<repo>/tags --jq '.[].name'
```

| State | Label |
|-------|-------|
| One or more tags | PASS |
| No tags | WARN — cannot be pinned to a specific release |

### 5. Freshness

```bash
npx skills check
```

| State | Label |
|-------|-------|
| Up to date | PASS |
| Update available (pinned) | INFO — update requires deliberate promotion |
| Update available (unpinned) | WARN — will drift on next install |

### 6. SKILL.md Structure

For skills installed from known sources, verify required frontmatter:

| Field | Required |
|-------|----------|
| `name` | Yes |
| `description` | Yes |

Missing fields → FAIL.

## Output Format

```
Skill Audit Report
Generated: 2026-06-10
Environment: production / project-scope

Skill: prechecks (owner/prompt-workbench)
  [PASS] Pinned to SHA abc1234
  [PASS] Install count: 12K
  [PASS] Source: trusted (owner)
  [PASS] Tagged releases: v1.0.0, v1.1.0
  [PASS] Up to date
  [PASS] SKILL.md valid

Skill: some-other-skill (unknown-author/random-repo)
  [FAIL] Unpinned (latest) — non-reproducible in production
  [FAIL] Install count: 47 — treat as experimental
  [FAIL] Source: unknown author, 12 GitHub stars
  [WARN] No tagged releases — cannot be pinned
  [WARN] Update available
  [PASS] SKILL.md valid

Summary
-------
Skills audited: 2
Passed: 1
Warnings: 0
Failures: 1

Recommended actions:
1. Pin or remove "some-other-skill" before promoting to production.
```

## Using This as a CI Step

Add a step to your CI workflow that runs the audit and fails the build on any FAIL result:

```yaml
- name: Skill Audit
  run: npx skills check && echo "Manual audit: review skills-lock.json for unpinned entries"
```

A fully automated audit script can be scaffolded using `npx skills init skill-audit-script` once your team stabilizes the lock format.

## Clarifying Questions to Ask Before Running

- Is this audit for a personal install or a production team environment?
- Should warnings block a PR merge, or are they advisory only?
- Are there internal/private skills that should be excluded from source reputation checks?

## Evidence Basis

- `npx skills check` for freshness from https://skills.sh/docs
- `gh api repos/.../tags` for release tag enumeration from GitHub REST API docs
- Supply-chain risk framing adapted from: "Skill supply-chain research warns that skill metadata and natural-language instructions can influence discovery, selection, and governance" (prompt-workbench-plan.md, External Best Practices Reviewed section)

This audit is a checklist tool, not a security scanner. It does not analyze skill content for malicious instructions.
