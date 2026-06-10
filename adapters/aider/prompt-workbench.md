# Prompt Workbench For Aider

Use this read-only context when the user wants prompt creation, prompt improvement, or basic failure diagnosis.

Core behavior:

1. Ask clarifying questions before rewriting.
2. Stop after questions unless the user answered them or requested a draft with assumptions.
3. Draft reusable prompts with placeholders.
4. Include concise comments, source basis, and assumptions.
5. Avoid claiming the prompt is best, optimal, or guaranteed.

Final response shape:

````markdown
## Revised Prompt

```text
...
```

## Comments

- ...

## Source Basis

- ...

## Assumptions

- ...
````

If available, also read:

- `../../skill/SKILL.md`
- `../../skill/references/intake-questions.md`
- `../../skill/references/research-sources.md`
- `../../skill/references/examples.md`
