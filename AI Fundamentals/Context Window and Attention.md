---
tags:
	- ai-fundamentals
	- context-window
	- attention
category: AI Fundamentals
related: Neural Networks and Transformers, Word Tokenization, Prompt Engineering Basics
---

# Context Window and Attention

The context window is the maximum amount of tokenized input and generated output a model can consider in one request. Attention is the mechanism that helps a transformer weigh relationships between tokens within that context.

## Context Window

A request consumes tokens from several sources:

```text
System instructions + conversation + retrieved content + user prompt + output
```

The total must fit within the model's supported context. A larger context window allows more material to be supplied, but it does not guarantee that every detail will receive equal attention or be used correctly.

## Attention

Self-attention allows each token representation to incorporate information from other tokens. In a sentence about a variable, for example, attention can help connect a later reference to the earlier declaration.

The simplified attention operation is:

$$
\operatorname{Attention}(Q,K,V) = \operatorname{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

Queries represent what a token is looking for, keys represent what other tokens offer for matching, and values contain the information that is combined.

## Context Budgeting

When a model has a maximum context $C$, prompt design must leave room for the expected answer:

$$
	ext{input tokens} + \text{reserved output tokens} \leq C
$$

Long files, repeated instructions, old conversation turns, and large retrieved documents consume the budget. Token limits depend on the specific model and provider, so measure with the relevant tokenizer or API usage data.

## Context Management Strategies

- **Summarization** - Compress earlier discussion while preserving decisions and constraints.
- **Chunking** - Split large documents into meaningful sections.
- **Retrieval** - Select relevant sections for the current question.
- **Filtering** - Remove duplicated, stale, or irrelevant material.
- **Structured state** - Store goals, decisions, files, and test results in compact fields.
- **Sliding window** - Retain the most relevant recent portion of a long stream.

Retrieval should preserve enough surrounding context to avoid changing the meaning of a code block, table, or paragraph.

## Long-Context Limitations

Models can lose accuracy when important information is buried among large amounts of irrelevant content. Repeating a fact does not guarantee correct use, and placing instructions near relevant content can sometimes improve reliability. Evaluation should test the actual document sizes and positions used by the application.

## Prompt Design for Attention

- Put the task and success criteria in clear, explicit language.
- Label sources, instructions, examples, and untrusted content.
- Use headings and delimiters to separate documents.
- Keep related evidence together.
- Ask the model to cite or identify the source of important claims.
- Reserve output space before adding more context.

## Context in Agentic Systems

Agents must manage context across tool calls. Include current state, tool results, constraints, and the next decision without replaying every historical message. Durable project memory can live in issues, files, or databases while the working context contains only what the next step requires.

## Related Concepts

- [[Neural Networks and Transformers]] - Transformer architecture and self-attention
- [[Word Tokenization]] - Count and manage input units
- [[Prompt Engineering Basics]] - Organize instructions and evidence
- [[Probabilistic and Vectorial nature]] - Representations and generation
- [[Agentic Architecture]] - Context management in tool-using workflows
