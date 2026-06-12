# Intake Questions

Use the smallest useful subset. Prefer 3-7 questions for ambiguous requests and fewer when the user already provided strong context.

## Prompt Creation

0. What kind of prompt do you need?
   - **System prompt** — sets the model's persona, behavior, and constraints once; not repeated per request
   - **User prompt** — the per-request message the model receives each time; often uses placeholders
   - **Both** — a full prompt architecture: system sets context, user carries the variable input

1. What should the model accomplish?
2. Who is the output for?
3. What input will the model receive each time?
4. What must the output include or avoid?
5. What format, length, tone, or structure should the output use?
6. Should the prompt include placeholders for repeated use?
7. Are there examples of good or bad outputs to match or avoid?

## Prompt Improvement

1. What is the current prompt?
2. What does "better" mean for this prompt: accuracy, completeness, tone, structure, speed, creativity, or something else?
3. What context does the model need that is not in the prompt?
4. What output format should the model follow?
5. What parts of the current prompt must be preserved?
6. What repeated inputs should become placeholders?

## Failure Diagnosis

1. What prompt did you use?
2. What output did it produce?
3. What output did you expect instead?
4. What was unacceptable about the current output?
5. Did the model miss context, ignore constraints, use the wrong tone, hallucinate, or format the answer incorrectly?
6. Are there constraints the model should treat as mandatory?

## Beginner-Friendly Explanation

When the user seems new to prompting, add one sentence before the questions:

"These questions help me avoid guessing about your goal, audience, and output format before I rewrite the prompt."
