---
name: prompt-workbench
description: Guided prompt creation, refinement, and basic failure diagnosis. Use when Codex needs to turn a rough user idea into a reusable prompt, improve an existing prompt, diagnose why a prompt produced a bad output, ask clarifying questions before rewriting, add placeholders, provide concise comments, and include a short source-basis and assumptions section.
---

# Prompt Workbench

## Core Rule

Ask clarifying questions before producing a final prompt. Stop after the questions unless the user has already answered them or explicitly asks for a draft with assumptions.

Use a concise coaching tone. Avoid claiming that a prompt is best, optimal, or guaranteed unless the prompt has been tested against stated criteria.

## Workflow

1. Classify the task as prompt creation, prompt improvement, or failure diagnosis.
2. Restate the understood goal in one sentence when the user gave only a rough idea.
3. Ask the minimum useful clarification questions. Use `references/intake-questions.md` when the task is ambiguous.
4. Check source basis before making important prompt-design claims. Use `references/research-sources.md`; use accessible public sources only when needed and available.
5. Rewrite or draft the prompt with reusable placeholders such as `{audience}`, `{input}`, `{constraints}`, `{examples}`, or `{output_format}`.
6. Add concise comments explaining the most important changes.
7. State assumptions instead of silently inventing missing requirements.
8. Add runtime notes only when the user's target runtime affects how the prompt should be used.
9. After producing the output, self-assess the draft for: non-trivial assumptions made, undefined `{placeholders}`, open-ended output format, pattern-sensitive tasks without examples, or a critical absent constraint. If any apply, append `## Follow-Up` (see Output Shape). Skip when none apply or when the user said "draft with assumptions" or "no more questions".

## Task Modes

### Create From Idea

Use when the user has a goal but no prompt.

Ask about prompt role first (system, user, or both) — see `references/intake-questions.md` Q0. Then ask about the task, audience, inputs, constraints, desired output format, and any examples. Draft accordingly:
- System prompt only: persona, behavior rules, output constraints, no per-request placeholders
- User prompt only: task instruction + placeholders for variable inputs
- Both: draft each section separately, clearly labeled

### Improve Existing Prompt

Use when the user provides a current prompt.

Identify likely weaknesses such as vague goals, missing context, hidden success criteria, weak output format, conflicting constraints, or ambiguous references. Ask clarifying questions before rewriting. Preserve the user's intent, not necessarily their wording.

### Diagnose Failed Prompt

Use when the user provides a current prompt, current output, expected output, and optional notes.

Compare the current output with the expected output. Identify likely prompt-specification issues separately from possible model limitations. Ask any missing clarification questions, then rewrite the prompt to reduce the observed failure.

After the user answers clarifying questions, always produce a `## Failure Diagnosis` section before the revised prompt. The diagnosis must explain what caused the bad output and why — not just what changed in the rewrite. This is required even when the cause seems obvious.

## Output Shape

If clarification is still needed, use:

```markdown
## Clarifying Questions

1. ...
2. ...
```

After the user answers, or when explicitly drafting with assumptions, use:

For **Create From Idea** and **Improve Existing Prompt**, label the output section based on role:

- System prompt only → use `## System Prompt`
- User prompt only → use `## User Prompt Template`
- Both → use two consecutive sections: `## System Prompt` then `## User Prompt Template`
- Role not specified and cannot be inferred → use `## Revised Prompt` and note the assumption

For **Diagnose Failed Prompt** only, prepend before the revised prompt:

````markdown
## Failure Diagnosis

- Root cause: ...
- Why the model produced the observed output: ...
````

Then continue with the standard output:

````markdown
## Revised Prompt

```text
...
```

## Comments

- ...

## Source Basis

- ...

## Runtime Notes

- ...

## Assumptions

- ...
````

`## Follow-Up` is appended **after** the closing of the standard output block above — it is not inside the template. Append it when triggered (see step 9):

````markdown
## Follow-Up

To verify my understanding:        ← include only if verification questions exist
- [one question per non-obvious assumption — max 2]

To improve the prompt:             ← include only if improvement questions exist
- [one question per open-ended area that could be tightened — max 2]
````

Only include a sub-header when that category has at least one question. Never render an empty sub-header.

**Triggers** (append if any are true):
- `## Assumptions` is non-empty
- Draft contains `{placeholders}` the user never defined
- Output format is open-ended (no structure, length, or shape specified)
- No examples in the draft but task is pattern-sensitive (classification, tone, style)
- A critical constraint is absent whose omission would likely cause wrong output (e.g. no error handling for a required edge case, no exclusion for a known failure mode)

Each question must be actionable — the user's answer should directly change something in the prompt. Do not repeat questions already asked in `## Clarifying Questions`.

Omit `Runtime Notes` when there are no runtime-specific concerns. Keep the source basis short and honest; "Bundled prompt-workbench notes; source not externally verified" is acceptable for phase 1 when no better source is available.

## Prompt Design Defaults

- Make the goal explicit.
- Separate context, task, constraints, and output format.
- Replace vague wording with observable requirements.
- Use placeholders for reusable inputs.
- Add simple JSON-shaped output instructions only when the user needs parseable output.
- Prefer examples only when they reduce ambiguity.
- Distinguish evidence-backed guidance from unverified heuristics.

## References

- Load `references/intake-questions.md` for question sets by scenario.
- Load `references/research-sources.md` for phase 1 source notes and source-priority rules.
- Load `references/examples.md` when the user would benefit from a short before/after pattern.
