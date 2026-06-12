# Examples

Use these as compact patterns, not as a template library.

## Rough Idea To Prompt

User idea:
"Help me summarize customer calls."

Useful rewrite pattern:

```text
You are helping summarize customer support calls for {audience}.

Context:
- Call transcript: {transcript}
- Product or account context: {context}

Task:
Summarize the call in a way that helps {audience} decide next actions.

Output:
1. Customer goal
2. Main issues
3. Promised follow-ups
4. Risks or unresolved questions
5. Recommended next action
```

## Existing Prompt Improvement

Weak prompt:
"Make this email better."

Useful rewrite pattern:

```text
Revise the email below for {audience}. Keep the meaning, make the tone {tone}, and keep it under {length}.

Email:
{email}

Return:
- Revised email
- 3 brief notes explaining important changes
```

## System + User Prompt

User goal:
"A code review assistant that checks for Python 3 compatibility."

System prompt:
```text
You are a Python code reviewer focused on Python 3 compatibility.
Flag any Python 2-only APIs, syntax, or patterns.
For each issue: name the line, explain why it fails in Python 3, and suggest the fix.
Do not comment on style or logic unless it is also a compatibility issue.
```

User prompt template:
```text
Review the following Python code for Python 3 compatibility issues.

Code:
{code}
```

## Failure Diagnosis

Observed failure:
The model gave a long essay when the user expected machine-readable output.

Useful rewrite pattern:

```text
Extract the requested fields from {input}. Return only valid JSON matching this shape:

{
  "summary": "string",
  "priority": "low | medium | high",
  "open_questions": ["string"]
}

If a field is unknown, use null instead of guessing.
```
