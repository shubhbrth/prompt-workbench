# Claude Adapter

## Install

Use `../../skill` as the Agent Skill folder. If the runtime requires the folder name to match the skill name, install it as `prompt-workbench` while preserving `SKILL.md` and `references/`.

## Invocation

Ask Claude or Claude Code to use the Prompt Workbench skill for prompt creation, prompt improvement, or failure diagnosis. Slash-command behavior, if available, is runtime-specific.

## Loading Behavior

Claude-style skill runtimes can load `SKILL.md` first and supporting references as needed. The canonical workflow is intentionally platform-neutral.

## Smoke Test

Ask: `Use the prompt-workbench skill to create a prompt from this idea: I want an assistant to turn meeting notes into action items.`

Expected: Claude asks clarification questions before drafting, then returns the final prompt with comments, source basis, and assumptions after answers are supplied.

## Limitations

Web search, local file access, and slash-command support depend on the user's Claude environment.
