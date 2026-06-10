# Aider Smoke Test

Prompt:

```text
Using the prompt-workbench context, diagnose why this prompt gave a vague answer:

Prompt: "Plan my project."
Output: "Make a plan."
Expected output: "A milestone plan with owners, deadlines, dependencies, and risks."
```

Expected behavior:

- Identify the missing scope, context, constraints, and output format.
- Ask clarification questions if needed.
- Return a revised prompt with comments, source basis, and assumptions.
