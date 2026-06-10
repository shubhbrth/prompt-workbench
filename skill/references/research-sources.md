# Research Sources

Phase 1 keeps this source basis intentionally small. Use these notes to support basic prompt-design choices, and mark limitations when no external lookup is available.

## Source Priority

1. User-provided examples, papers, internal docs, or evaluation results.
2. Official provider documentation relevant to the user's target model or platform.
3. Survey papers or research papers about prompting techniques.
4. Reputable technical articles with concrete examples or evaluations.
5. General model knowledge, marked as unverified, when no better source is available.

## Bundled Notes

- Clear task framing, relevant context, constraints, and output-format instructions usually reduce ambiguity and make the model's target behavior easier to follow.
- Few-shot examples can help when the desired style, reasoning pattern, or output structure is hard to describe, but unnecessary examples can add noise.
- Structured-output instructions should be simple in phase 1. Use JSON-shaped examples only when the user needs parseable output.
- Prompt behavior varies by model and runtime. Avoid universal claims unless backed by user tests or runtime-specific documentation.
- Failure diagnosis should compare actual and expected output before rewriting, because the same bad output can come from missing context, weak constraints, ambiguous success criteria, or model limitations.

## Source-Basis Wording

Use short, transparent entries such as:

- "Bundled prompt-workbench notes: make task, context, constraints, and output format explicit."
- "User-provided expected output: rewrite focuses on the observed mismatch."
- "Source not externally verified in this runtime; recommendation is a conservative prompt-design heuristic."

## Refresh Search Terms

- official prompt engineering guide task context output format
- prompt engineering survey structured output examples
- LLM prompt sensitivity failure modes
- provider documentation JSON structured outputs prompting
