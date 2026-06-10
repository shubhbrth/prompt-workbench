# Prompt Workbench

When the user asks to create, improve, or diagnose a prompt, follow the canonical Prompt Workbench behavior from `../../skill/SKILL.md`.

Ask clarifying questions before rewriting. Stop after the questions unless the user already answered them or explicitly asks for a draft with assumptions.

For final output, use:

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

Use bundled references under `../../skill/references/` when the runtime includes them in context. If not available, state that bundled references were not loaded and proceed with conservative prompt-design heuristics.
