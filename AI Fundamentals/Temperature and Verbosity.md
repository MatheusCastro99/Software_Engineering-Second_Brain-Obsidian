---
tags:
	- ai-fundamentals
	- llm
	- generation
category: AI Fundamentals
related: Probabilistic and Vectorial nature, Prompt Engineering Basics, Word Tokenization
---

# Temperature and Verbosity

Temperature and verbosity are generation controls that affect how an AI model selects and presents output. Temperature primarily influences variation in token selection; verbosity describes the amount of detail, explanation, and text requested or produced.

## Temperature

Before sampling the next token, a model can adjust its logits using a temperature value $T$:

$$
P_T(i) = \frac{e^{z_i/T}}{\sum_j e^{z_j/T}}
$$

where $z_i$ is the score for token $i$.

- **Lower temperature** makes high-probability choices more dominant and output more predictable.
- **Higher temperature** flattens the distribution and allows less likely choices more often.
- **Temperature zero or near zero** typically favors deterministic or greedy selection, although exact behavior depends on the system.

Temperature does not add knowledge or improve reasoning by itself. It changes the selection behavior of the generation process.

## Choosing a Temperature

| Task | General preference | Reason |
|------|--------------------|--------|
| JSON or code generation | Low | Consistency and format compliance |
| Classification | Low | Stable labels and decisions |
| Summarization | Low to moderate | Faithful wording with readable variation |
| Brainstorming | Moderate to high | More diverse possibilities |
| Creative writing | Moderate to high | Novel phrasing and variation |

The available range and meaning of temperature vary by model provider. Test the setting with representative inputs rather than assuming values transfer between models.

## Verbosity

Verbosity is the level of detail in an answer. It is influenced by the prompt, model behavior, context, output-token limits, and interface defaults.

```text
Low verbosity: Give the command only.
Moderate verbosity: Give the command and one sentence explaining it.
High verbosity: Explain the command, alternatives, risks, and examples.
```

Specify the intended audience and output shape instead of asking only for a vague amount of detail:

```text
Explain this to a junior developer in five bullets, including one example
and one common mistake. Do not include a general introduction.
```

## Temperature vs. Verbosity

These controls solve different problems. Increasing temperature does not reliably make an answer longer, and reducing verbosity does not necessarily make an answer more accurate. Use instructions for length and detail; use sampling settings for variation and predictability.

## Practical Tuning Process

1. Define what a successful response looks like.
2. Choose a low-variation setting for structured or repeatable work.
3. Test several representative and edge-case prompts.
4. Measure correctness, format compliance, usefulness, and length.
5. Change one variable at a time.

For production systems, log model and generation settings with evaluation results. A setting that works for one task may be unsuitable for another.

## Common Misunderstandings

- Low temperature does not guarantee factual correctness.
- High temperature does not create independent reasoning.
- More words do not necessarily mean more useful information.
- A token limit can truncate a concise answer if the context is already large.
- Provider names such as "creative" or "balanced" may map to different internal settings.

## Related Concepts

- [[Probabilistic and Vectorial nature]] - Token probabilities and vector representations
- [[Prompt Engineering Basics]] - Request a useful level of detail
- [[Word Tokenization]] - Understand output limits
- [[Agentic Architecture]] - Control generation in tool-using workflows
