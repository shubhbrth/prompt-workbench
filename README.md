<div align="center">

# prompt-workbench

**Guided prompt engineering skill — create, improve, and diagnose prompts
with clarifying questions and cited sources, across 12+ agent runtimes**

</div>

<div align="center">

[![npx install](https://img.shields.io/badge/install-npx_skills-blue?logo=npm&logoColor=white)](https://skills.sh)
[![SKILL.md](https://img.shields.io/badge/format-SKILL.md-brightgreen)](skill/SKILL.md)
[![Runtimes](https://img.shields.io/badge/runtimes-12%2B-orange)](#supported-runtimes)
[![Version](https://img.shields.io/github/v/release/shubhbrth/prompt-workbench)](https://github.com/shubhbrth/prompt-workbench/releases)

</div>

<div align="center">

[Installation](#installation) • [Quick Start](#quick-start) • [How It Works](#how-it-works) • [Usage Examples](#usage-examples) • [Companion Skills](#companion-skills) • [Roadmap](#roadmap)

</div>

---

## Quick Start

```bash
npx skills add shubhbrth/prompt-workbench@prompt-workbench
```

Then tell your agent what you need:

- **Create** — describe a goal → get a reusable prompt with clarifying questions first
- **Improve** — paste an existing prompt → get a rewrite with change comments
- **Diagnose** — share prompt + bad output + expected output → get a targeted fix

## Installation

### Step 1 — Check your prerequisites

Before installing, confirm the tools you need are available:

```bash
node --version   # Required for both paths — must be 18+
npx --version    # Required for Option A — included with Node.js
gh --version     # Required for Option B only
gh auth status   # Required for Option B only — run `gh auth login` if not logged in
```

If Node.js is missing: install from https://nodejs.org (LTS release)  
If gh CLI is missing: install from https://cli.github.com

---

### Step 2 — Pick your install path

| I want to… | Use |
|------------|-----|
| Install for myself, any agent, any OS | **Option A — npx** |
| Share skills with a team via git | **Option B — gh CLI, project scope** |
| Lock to a specific version (production) | **Option B — gh CLI, pinned** |
| Not sure | **Option A — npx** |

---

### Option A — npx (personal use, any OS)

**1. Install the core skill:**
```bash
npx skills add shubhbrth/prompt-workbench@prompt-workbench
```

**2. Install companion skills (optional but recommended):**
```bash
npx skills add shubhbrth/prompt-workbench@prechecks       # env validation
npx skills add shubhbrth/prompt-workbench@mlops-workflow   # team versioning model
npx skills add shubhbrth/prompt-workbench@skill-audit      # production hygiene checks
```

**3. Verify everything installed correctly:**
```bash
npx skills list
```

> **Note:** `npx skills check` has known bugs in v1.5.10 on Windows (shorthand clone failure and unquoted path in subprocess). Use `npx skills add` to manually update skills until a fix is released.

---

### Option B — GitHub CLI (team or production use)

Choose **one** sub-path based on your need. Do not combine them.

#### B1 — Personal install via gh CLI

```bash
gh skill install shubhbrth/prompt-workbench prompt-workbench --agent claude-code --scope user
gh skill install shubhbrth/prompt-workbench prechecks       --agent claude-code --scope user
gh skill install shubhbrth/prompt-workbench mlops-workflow  --agent claude-code --scope user
gh skill install shubhbrth/prompt-workbench skill-audit     --agent claude-code --scope user
```

#### B2 — Team install (shared via git)

Installs into `.agents/skills/` in your repo. Commit this folder so teammates get the same skills.

```bash
gh skill install shubhbrth/prompt-workbench prompt-workbench --agent claude-code --scope project
gh skill install shubhbrth/prompt-workbench prechecks        --agent claude-code --scope project
gh skill install shubhbrth/prompt-workbench mlops-workflow   --agent claude-code --scope project
gh skill install shubhbrth/prompt-workbench skill-audit      --agent claude-code --scope project

git add .agents/skills/
git commit -m "chore: add prompt-workbench skills"
```

#### B3 — Production install (pinned to a specific version)

Use a version tag or commit SHA so the skill never changes unexpectedly.

```bash
gh skill install shubhbrth/prompt-workbench prompt-workbench --pin v1.0.0 --agent claude-code --scope project
gh skill install shubhbrth/prompt-workbench prechecks        --pin v1.0.0 --agent claude-code --scope project
gh skill install shubhbrth/prompt-workbench mlops-workflow   --pin v1.0.0 --agent claude-code --scope project
gh skill install shubhbrth/prompt-workbench skill-audit      --pin v1.0.0 --agent claude-code --scope project

git add .agents/skills/
git commit -m "chore: pin prompt-workbench skills to v1.0.0"
```

To roll back to a previous version, replace `v1.0.0` with the earlier tag or commit SHA.

---

## Companion Skills

Three production-readiness skills ship alongside the core prompt-workbench skill:

| Skill | What it does | When to install |
|-------|-------------|-----------------|
| `prechecks` | Validates your environment before any skill install or session | Always — install first |
| `mlops-workflow` | 3-stage dev → staging → production promotion model for skills | Team / production use |
| `skill-audit` | Audits installed skills for version pins, source trust, and freshness | Before releases or PR merges |

## Supported Runtimes

| Runtime | Primary packaging | Secondary |
|---------|------------------|-----------|
| Codex | `SKILL.md` | `AGENTS.md` |
| Claude / Claude Code | `SKILL.md` | `CLAUDE.md`, `AGENTS.md` |
| Gemini CLI | `GEMINI.md` or `AGENTS.md` | settings.json context config |
| Antigravity | `AGENTS.md`-style instructions | verifiable artifacts |
| Cursor | `AGENTS.md` | Cursor rules |
| Windsurf / Devin Desktop | `.devin/rules/*.md`, `AGENTS.md` | skills, workflows |
| Cline | `.clinerules/*.md`, `AGENTS.md` | `.cursorrules`, `.windsurfrules` |
| Roo Code | `.roo/rules/*.md`, `AGENTS.md` | `.roorules`, mode rule folders |
| Continue | `.continue/rules/*.md` | Hub rules |
| GitHub Copilot | `.github/copilot-instructions.md` | `AGENTS.md`, `.instructions.md` |
| Aider | `--read prompt-workbench.md` | `.aider.conf.yml` read entry |
| Other agents | `AGENTS.md` | manual Markdown reference |

## Repo Structure

```
prompt-workbench/
├── .github/
│   └── workflows/
│       └── validate-skills.yml     # CI: validates all SKILL.md frontmatter
├── skill/
│   ├── SKILL.md                    # canonical platform-neutral skill
│   └── references/
│       ├── intake-questions.md
│       ├── prompt-patterns.md
│       ├── failure-diagnosis.md
│       ├── research-sources.md
│       └── examples.md
├── skills/                         # all skills (standard discovery location)
│   ├── prompt-workbench/SKILL.md   # core skill (npx skills discoverable)
│   ├── prechecks/SKILL.md
│   ├── mlops-workflow/SKILL.md
│   └── skill-audit/SKILL.md
├── adapters/
│   ├── codex/README.md
│   ├── claude/README.md
│   ├── gemini-cli/
│   ├── antigravity/
│   ├── agents-md/AGENTS.md
│   ├── cursor/
│   ├── windsurf-devin/
│   ├── cline/
│   ├── roo-code/
│   ├── continue/
│   ├── github-copilot/
│   └── aider/
└── smoke-tests/
```

## How It Works

The skill always asks clarifying questions before producing a revised prompt — even when you say "just improve this." This is intentional: you should understand and control the improvement, not receive a black-box rewrite.

**Three workflows:**

1. **Create** — you describe a goal, the skill asks 3–7 targeted questions, then produces a reusable prompt with comments and source basis
2. **Improve** — you paste an existing prompt, the skill identifies weaknesses, asks clarifying questions, then rewrites with change comments
3. **Diagnose** — you provide current prompt + current output + expected output, the skill identifies failure causes and rewrites to address them

**Output structure:**

```
## Clarifying Questions
## Revised Prompt
## Comments
## Source Basis
## Runtime Notes
## Assumptions
```

## Usage Examples

The examples below show the same three workflows in both Codex and Claude Code so you can see how the skill behaves in each runtime.

---

### Workflow 1: Create a prompt from an idea

You have a goal but no prompt yet.

#### In Codex

```
> Use prompt-workbench. I want a prompt that summarizes meeting notes into action items.
```

The skill responds with clarifying questions:

```
## Clarifying Questions

1. Who reads the action items — just you, or a team in a shared doc?
2. Should the output group items by owner, deadline, or topic?
3. How long are the meeting notes typically — a few bullet points or several paragraphs?
4. Is any tool involved (Notion, Jira, email)? Should the format match it?
5. Should the prompt include a placeholder for the meeting notes, or will you paste them inline?
```

After you answer, Codex produces:

```
## Revised Prompt

You are a meeting assistant. Summarize the following meeting notes into a list of action items.

For each action item include:
- Owner (the person responsible)
- Task (what needs to be done, one sentence)
- Deadline (if mentioned; otherwise write "not specified")

Format the output as a markdown table. Do not include discussion or context — only decisions and tasks.

Meeting notes:
{{meeting_notes}}

## Comments
- Separated owner/task/deadline because the user needs to assign items to teammates.
- Added "not specified" fallback so the table stays consistent even when deadlines are missing.
- Used a placeholder {{meeting_notes}} so the prompt is reusable.

## Source Basis
- Structured output guidance: Anthropic prompting docs — separating task from format instructions reduces hallucination risk.
```

---

#### In Claude Code

```
> /prompt-workbench I want a prompt that summarizes meeting notes into action items.
```

The skill behaves identically — same clarifying questions, same output structure. The `/prompt-workbench` slash command triggers the skill in Claude Code.

---

### Workflow 2: Improve an existing prompt

You already have a prompt but it is not working well enough.

#### In Codex

```
> Use prompt-workbench to improve this prompt:
> "Summarize this text."
```

The skill identifies weaknesses first:

```
I can see a few issues before I rewrite:
- No goal stated — summarize for what purpose?
- No output format — bullet points, paragraph, one sentence?
- No length constraint — the model will guess
- No audience — tone and depth are unclear

## Clarifying Questions
1. What is the summary used for — a quick skim, a report, an email?
2. Should it be a single sentence, a short paragraph, or bullet points?
3. Who is the reader — yourself, a colleague, a non-technical stakeholder?
```

After you answer, the rewritten prompt:

```
## Revised Prompt

Summarize the following text for a non-technical stakeholder.
Write 3–5 bullet points. Each bullet should be one sentence.
Focus on decisions and outcomes — omit background and technical detail.

Text:
{{text}}

## Comments
- Added audience ("non-technical stakeholder") so tone and vocabulary adjust automatically.
- Specified bullet format and count to prevent open-ended responses.
- "Decisions and outcomes" replaces vague "summarize" — gives the model a clear filter.
```

---

#### In Claude Code

```
> /prompt-workbench improve this: "Summarize this text."
```

Same output. Claude Code loads the skill from `skill/SKILL.md` and runs the same improvement workflow.

---

### Workflow 3: Diagnose a failed prompt

Your prompt is producing wrong output and you need to understand why.

#### In Codex

```
> Use prompt-workbench to diagnose this.
>
> Current prompt: "Write a SQL query for the sales data."
> Current output: SELECT * FROM sales WHERE date > '2024-01-01'
> Expected output: A query that joins sales with customers and filters by region.
```

The skill diagnoses:

```
## Failure Diagnosis

The prompt is missing two things the model cannot infer:
1. Schema context — it does not know that a `customers` table exists or how it joins to `sales`.
2. Filter intent — "sales data" does not communicate that region filtering is needed.

The model defaulted to the simplest valid query it could construct from the prompt alone.

## Revised Prompt

Write a SQL query using the following schema:
- Table: sales (id, customer_id, amount, date, region)
- Table: customers (id, name, region, account_manager)

Requirements:
- Join sales to customers on customer_id = customers.id
- Filter by region: {{region}}
- Return: customer name, total sales amount, date
- Order by total sales amount descending

## Comments
- Added schema so the model knows what tables and columns exist.
- Made the join condition explicit — the model cannot infer foreign keys from table names alone.
- Added {{region}} placeholder so the prompt is reusable across regions.

## Source Basis
- Missing context is the most common cause of hallucinated SQL (Anthropic prompting docs — provide all facts the model cannot look up).
```

---

#### In Claude Code

```
> /prompt-workbench diagnose:
> prompt: "Write a SQL query for the sales data."
> output: SELECT * FROM sales WHERE date > '2024-01-01'
> expected: query joining sales with customers, filtered by region
```

Claude Code runs the same diagnosis. If you have web search enabled in your Claude Code session, the skill can also pull in current SQL prompting guidance from external sources and cite it in the Source Basis section.

---

### Key difference between runtimes

| | Codex | Claude Code |
|--|-------|-------------|
| How to invoke | `Use prompt-workbench` in chat | `/prompt-workbench` slash command |
| Skill loaded from | `skill/SKILL.md` | `skill/SKILL.md` |
| Web search | Depends on Codex tool config | Available if enabled in session |
| Output format | Identical | Identical |

The workflow and output are the same in both runtimes — only the invocation differs.

---

## What It Won't Do

- Guarantee a prompt is optimal or best — it says "evidence-backed" or "reasonable heuristic," not "proven"
- Give model-specific advice unless you provide your target model and sources
- Replace your judgment — it explains reasoning so you can accept, reject, or adapt
- Cover non-English prompts (deferred to future plan)
- Generate automated test cases by default

## Adding a New Runtime Adapter

1. Create `adapters/<runtime>/` with a `README.md` and the runtime's required file format
2. Follow the adapter quality bar in the planning docs (installation path, instruction loading, web search availability, known limitations, smoke test)
3. Point back to `skill/SKILL.md` for canonical workflow — do not fork behavior
4. Open a PR — CI will validate all `SKILL.md` frontmatter automatically

## Roadmap

### Available now
- ✅ Create a prompt from a rough idea (guided, with clarifying questions)
- ✅ Improve an existing prompt (restructure, clarify, add placeholders)
- ✅ Diagnose a failed prompt from observed output vs expected output
- ✅ Evidence-backed design choices with cited source basis
- ✅ Adapters for Codex, Claude Code, Gemini CLI, Aider, and generic AGENTS.md
- ✅ Companion skills: prechecks, mlops-workflow, skill-audit
- ✅ CI validation for all SKILL.md files on every PR

### Planned
- 📋 Expanded prompt pattern reference (structured output, reasoning prompts, few-shot)
- 📋 Failure diagnosis reference with common failure types and rewrites
- 📋 Web search integration for live evidence retrieval
- 📋 Multi-variant prompt generation on request
- 📋 Prompt safety and injection-defense workflow
- 📋 Non-English prompt support

Found a gap or want to add a runtime adapter? Open an issue or PR.
