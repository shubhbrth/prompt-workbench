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

The examples below show the same three workflows in both Codex and Claude Code. The scenario: a developer building an AI-powered customer support feature.

---

### Workflow 1: Create a prompt from an idea

You need a system prompt for a chatbot but have nothing written yet.

#### In Codex

```
> Use prompt-workbench. I need a system prompt for a customer support chatbot
> that handles refund requests for a SaaS product.
```

The skill asks clarifying questions before writing anything:

```
## Clarifying Questions

1. Should the bot resolve refunds autonomously, or escalate to a human agent after gathering info?
2. What refund policy rules must the bot enforce — time limit, eligibility criteria, exceptions?
3. What tone: formal and professional, or friendly and conversational?
4. Does the bot have access to order/account data, or does it need to ask the user for it?
5. What should the bot do when a request falls outside the refund policy?
```

After you answer, Codex produces:

```
## Revised Prompt

You are a customer support assistant for {{product_name}}. Your role is to help
customers with refund requests according to the policy below.

Refund policy:
{{refund_policy}}

Instructions:
- Greet the customer and ask for their order ID if not already provided.
- Check whether the request is within 30 days of purchase and for an eligible plan.
- If eligible: confirm the refund and provide a reference number.
- If ineligible: explain the reason clearly and offer an alternative (credit, extension).
- Do not process refunds for accounts with open fraud flags — escalate to a human agent.
- Keep responses under 100 words. Use a professional but empathetic tone.

## Comments
- Separated policy from instructions so the policy can be updated without rewriting the prompt.
- Added explicit escalation rule for fraud flags — the model cannot infer this from context.
- Used {{product_name}} and {{refund_policy}} placeholders so the prompt is reusable across products.

## Source Basis
- Instruction/data separation: Anthropic prompting docs — mixing policy rules with instructions
  increases the chance the model blends or ignores them.
```

---

#### In Claude Code

```
> /prompt-workbench I need a system prompt for a customer support chatbot
> that handles refund requests for a SaaS product.
```

Same clarifying questions, same output structure. The `/prompt-workbench` slash command triggers the skill in Claude Code.

---

### Workflow 2: Improve an existing prompt

You already have a system prompt but the bot gives inconsistent answers.

#### In Codex

```
> Use prompt-workbench to improve this prompt:
>
> "You are a helpful assistant. Answer customer questions about our product
>  and help them with any issues they have."
```

The skill identifies weaknesses before rewriting:

```
I can see several issues before I rewrite:
- No role boundary — "any issues" is unbounded, the model will attempt anything
- No tone or length guidance — responses will vary in style and length
- No escalation path — the model will guess when to hand off to a human
- No product context — the model has no basis for accurate answers

## Clarifying Questions
1. What topics should the bot handle, and what should it explicitly decline?
2. Should it ever transfer to a human agent — if so, under what conditions?
3. What is the target response length: concise (1–3 sentences) or detailed?
4. Is there a knowledge base or documentation the bot should reference?
```

After you answer, the rewritten prompt:

```
## Revised Prompt

You are a customer support assistant for {{product_name}}. You help customers
with billing questions, account access, and plan changes.

Scope:
- Answer questions about billing, subscriptions, and account settings.
- Do not provide legal, security, or engineering advice — redirect to the relevant team.
- If the customer is frustrated or the issue is unresolved after two exchanges, offer to
  connect them with a human agent.

Use a friendly, concise tone. Keep responses under 80 words unless the customer asks
for more detail.

## Comments
- Added explicit scope so the model knows what to decline, not just what to help with.
- Defined the escalation trigger (two unresolved exchanges) rather than leaving it to judgment.
- Length constraint prevents verbose responses that frustrate support customers.

## Source Basis
- Scope constraints reduce off-topic responses: Anthropic prompting docs — tell the model
  what not to do as explicitly as what to do.
```

---

#### In Claude Code

```
> /prompt-workbench improve this:
> "You are a helpful assistant. Answer customer questions about our product
>  and help them with any issues they have."
```

Same output. Claude Code loads the skill from `skill/SKILL.md` and runs the same improvement workflow.

---

### Workflow 3: Diagnose a failed prompt

Your code generation prompt keeps producing Python 2 syntax instead of Python 3.

#### In Codex

```
> Use prompt-workbench to diagnose this.
>
> Current prompt: "Write a Python function that reads a CSV file and returns
>                  a list of rows where the status column equals 'active'."
> Current output: Uses `print "done"`, `unicode()`, and opens files without encoding param.
> Expected output: Python 3 syntax — f-strings, open() with encoding="utf-8", print().
```

The skill asks clarifying questions before diagnosing:

```
## Clarifying Questions

1. Which model are you sending this to — does it default to Python 2 examples in training?
2. Should the function handle large files (streaming) or is loading into memory acceptable?
3. What CSV library should it use: stdlib `csv`, `pandas`, or no preference?
4. Should the function raise errors on missing columns, or silently skip them?
```

After you answer, the skill diagnoses and rewrites:

```
## Failure Diagnosis

The prompt does not specify a Python version. When unspecified, some models default to
Python 2-compatible syntax — especially for file I/O and print statements, where Python 2
patterns are common in training data.

## Revised Prompt

Write a Python 3.8+ function that reads a CSV file and returns a list of rows where
the `status` column equals "active".

Requirements:
- Use the stdlib `csv` module.
- Open the file with `encoding="utf-8"`.
- Return a list of dicts (one per matching row).
- Raise a `ValueError` if the `status` column is not present in the header.
- Use type hints for the function signature.

## Comments
- Added "Python 3.8+" so the model cannot fall back to Python 2 patterns.
- Specified `encoding="utf-8"` explicitly — omitting it causes platform-dependent behavior.
- Added error handling requirement so the model does not silently swallow missing columns.

## Source Basis
- Version pinning prevents training-data ambiguity: models trained on mixed Python 2/3 corpora
  default to older syntax when the version is unspecified (observed pattern, not guaranteed).
```

---

#### In Claude Code

```
> /prompt-workbench diagnose:
> prompt: "Write a Python function that reads a CSV file and returns rows where status = active."
> output: Uses Python 2 syntax — print statement, unicode(), no encoding param.
> expected: Python 3 — f-strings, open() with encoding, print function.
```

Same diagnosis workflow. If web search is enabled in your Claude Code session, the skill can pull current Python best-practice references and cite them in the Source Basis section.

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
- ✅ Prompt role intake — asks whether you need a system prompt, user prompt, or both before drafting
- ✅ Conditional follow-up questions — after drafting, asks targeted questions to verify assumptions and tighten open-ended areas

### Planned
- 📋 Expanded prompt pattern reference (structured output, reasoning prompts, few-shot)
- 📋 Failure diagnosis reference with common failure types and rewrites
- 📋 Web search integration for live evidence retrieval
- 📋 Multi-variant prompt generation on request
- 📋 Prompt safety and injection-defense workflow
- 📋 Non-English prompt support

Found a gap or want to add a runtime adapter? Open an issue or PR.
