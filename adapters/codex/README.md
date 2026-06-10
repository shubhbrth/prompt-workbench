# Codex Adapter

## Install

Copy or symlink `../../skill` into a Codex skills directory as `prompt-workbench`, or invoke it manually by referencing `../../skill/SKILL.md`.

## Loading Behavior

Codex-style skill runtimes can use `SKILL.md` metadata for triggering and load reference files progressively. Keep `skill/agents/openai.yaml` with the skill if the runtime supports UI metadata.

## Source Access

Use bundled references first. Use web search only when available and needed for current, specialized, disputed, or model-specific prompt advice.

## Smoke Test

Ask: `Use $prompt-workbench to improve this prompt: "Write a report about our sales."`

Expected: Codex asks clarifying questions before rewriting and later returns a revised prompt, comments, source basis, and assumptions.

## Limitations

Phase 1 does not include automated tests, deep paper extraction, safety-specific prompt-injection workflows, or full runtime-specific guidance.
