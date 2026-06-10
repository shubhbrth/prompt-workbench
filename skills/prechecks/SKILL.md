---
name: prechecks
description: Validates the local environment before any skill install, skill update, or prompt-workbench session. Checks for required tools (node, npx, gh CLI), auth state, git repo presence, and network access. Surfaces pass/fail per check with a specific fix command for each failure.
---

# Prechecks

Validates the environment before any skill operation or prompt-workbench session. Run this before installing, updating, or publishing skills — especially in team or production contexts.

## When to Use This Skill

Use this skill when the user:

- Is about to install or update a skill for the first time on a machine
- Is setting up a new team member's environment
- Is debugging a failed skill install
- Is preparing to publish a skill to skills.sh
- Is onboarding a new agent runtime

## Checks

Run the following checks in order. Surface each result as pass or fail with a fix command.

### 1. Node.js and npx

```bash
node --version
npx --version
```

**Pass**: both return version strings  
**Fail fix**: Install Node.js (includes npx) from https://nodejs.org — use the LTS release

Minimum recommended version: Node.js 18+

### 2. Network Access

```bash
npx skills find --help
```

**Pass**: command returns help text without network errors  
**Fail fix**: Check your internet connection or proxy settings. If behind a corporate proxy, set `HTTP_PROXY` and `HTTPS_PROXY` environment variables.

### 3. gh CLI (required only for advanced path)

```bash
gh --version
```

**Pass**: returns version string  
**Fail fix**:
- Windows: `winget install GitHub.cli`
- macOS: `brew install gh`
- Linux: see https://cli.github.com/manual/installation

Skip this check if the user is only using the `npx skills` path.

### 4. gh Auth Status (required only for advanced path)

```bash
gh auth status
```

**Pass**: shows authenticated account  
**Fail fix**: `gh auth login` — follow the interactive prompts

Skip this check if the user is only using the `npx skills` path.

### 5. Git Repository (required only for project-scope installs)

```bash
git rev-parse --show-toplevel
```

**Pass**: returns the repo root path  
**Fail fix**: `git init` to create a repo, or navigate to an existing repo before running a project-scoped install

Skip this check if the user is doing a user-scoped (`-g` / `--scope user`) install only.

## Output Format

Report each check clearly:

```
Prechecks
---------
[PASS] Node.js v20.11.0
[PASS] npx 10.2.4
[PASS] Network access (skills.sh reachable)
[PASS] gh CLI 2.47.0
[PASS] gh auth (logged in as: user@example.com)
[PASS] Git repo (/path/to/repo)

All checks passed. Safe to proceed.
```

Or with failures:

```
Prechecks
---------
[PASS] Node.js v20.11.0
[PASS] npx 10.2.4
[FAIL] Network access — cannot reach skills.sh
       Fix: check connection or set HTTP_PROXY / HTTPS_PROXY
[SKIP] gh CLI (not needed for npx path)
[SKIP] gh auth (not needed for npx path)
[SKIP] Git repo (user-scope install — not required)

1 check failed. Resolve before proceeding.
```

## Evidence Basis

- Node.js LTS version requirement sourced from https://nodejs.org/en/about/releases/
- `gh auth status` behavior from https://cli.github.com/manual/gh_auth_status
- Skills.sh install standard from https://skills.sh/docs

Prechecks are environment-specific. Results on one machine do not guarantee the same on another.
