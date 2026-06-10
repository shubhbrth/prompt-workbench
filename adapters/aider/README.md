# Aider Adapter

## Use

Load the adapter as read-only context:

```bash
aider --read prompt-workbench.md
```

You can also load the canonical skill and references with additional `--read` arguments when useful.

## Loading Behavior

Aider does not need native skill discovery for this phase 1 package. The adapter is a manual context file.

## Smoke Test

Ask: `Using the prompt-workbench context, diagnose why this prompt gave a vague answer: prompt "Plan my project"; output "Make a plan"; expected output "A milestone plan with owners and deadlines."`

Expected: Aider asks clarifying questions or, if enough context is present, diagnoses the failure and returns a revised prompt with comments, source basis, and assumptions.

## Limitations

Reference files are available only if the user loads them or keeps them in accessible context.
