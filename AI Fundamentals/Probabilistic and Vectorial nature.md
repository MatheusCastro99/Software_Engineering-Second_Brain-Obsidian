---
tags:
	- ai-fundamentals
	- probability
	- vectors
	- machine-learning
category: AI Fundamentals
related: Word Tokenization, Temperature and Verbosity, Prompt Engineering Basics
---

# Probabilistic and Vectorial Nature of AI

Modern language models represent text as numerical vectors and generate output by assigning probabilities to possible next tokens. This explains both their ability to capture relationships in language and their inability to guarantee that every generated statement is true.

## From Text to Numbers

Computers cannot reason directly over words as human-readable symbols. A model converts text into tokens and maps those tokens, along with their context, into numerical representations called vectors or embeddings.

```text
Text -> Tokens -> Vector representations -> Model computation -> Token probabilities
```

Related meanings tend to occupy nearby regions of a learned vector space. Similarity can be estimated with measures such as cosine similarity:

$$
\operatorname{cosine\ similarity}(a,b) = \frac{a \cdot b}{\|a\|\|b\|}
$$

This is useful for semantic search, recommendations, clustering, and retrieval-augmented generation.

## Next-Token Probabilities

At each generation step, the model produces a probability distribution over the available vocabulary. Given the previous context, it estimates:

$$
P(\text{next token} \mid \text{previous tokens})
$$

The selected token is appended to the context, and the process repeats until a stopping condition is reached. The model is therefore generating a sequence one token at a time, even when the result appears to be a complete argument or program.

## Probability Is Not Truth

A likely continuation can be fluent, useful, or wrong. The model's probability reflects patterns learned from data and the current context, not direct access to truth. This is why generated output requires verification when accuracy matters.

Common causes of incorrect answers include:

- Missing or ambiguous context
- Outdated or incomplete training information
- Conflicting patterns in the source data
- A prompt that encourages unsupported assumptions
- The model filling a gap with a plausible continuation

## Vectors and Context

The same token can contribute to different meanings depending on nearby tokens. For example, `bank` in a financial sentence and `bank` in a river sentence receives different contextual representations. The model uses relationships between tokens, positions, and surrounding context rather than treating every word as an isolated dictionary entry.

## Practical Implications

- Give the model relevant context instead of relying on general knowledge.
- Ask for structured output when downstream code will parse the result.
- Use retrieval or source citations for knowledge that must be current.
- Validate generated code, calculations, and claims independently.
- Use embeddings for similarity tasks, not as a substitute for authorization or exact equality.

## A Simple Mental Model

Think of a language model as a probabilistic pattern generator operating over vector representations. It can reason through patterns and context, but it does not automatically possess intent, awareness, or a built-in truth checker.

## Related Concepts

- [[Word Tokenization]] - How text is divided before processing
- [[Temperature and Verbosity]] - How generation choices affect output
- [[Prompt Engineering Basics]] - Supply useful context and constraints
- [[Agentic Architecture]] - Use model output inside a controlled system
