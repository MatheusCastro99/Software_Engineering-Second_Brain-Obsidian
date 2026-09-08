---
tags:
	- ai-fundamentals
	- tokenization
	- llm
category: AI Fundamentals
related: Probabilistic and Vectorial nature, Temperature and Verbosity, Prompt Engineering Basics
---

# Word Tokenization

Tokenization is the process of converting text into the smaller units a language model reads and generates. A token may be a whole word, part of a word, punctuation, whitespace pattern, or special marker. Tokens are not the same as words.

## Example

The sentence:

```text
Unbelievable results!
```

Could be divided conceptually into pieces such as:

```text
["Un", "believ", "able", " results", "!"]
```

The exact result depends on the tokenizer and vocabulary used by the model. Different models can count the same text differently.

## Why Subword Tokens Are Used

A vocabulary containing every possible word would be very large and would fail on new words, names, code identifiers, and spelling variations. Subword tokenization balances vocabulary size with the ability to represent unfamiliar text.

Common approaches include:

- **Byte-pair encoding (BPE)** - Builds frequent symbol combinations into tokens.
- **WordPiece** - Selects subword units based on likelihood and vocabulary construction.
- **Unigram models** - Choose a probable segmentation from candidate pieces.
- **Byte-level tokenization** - Represents arbitrary text and avoids unknown characters.

## Token IDs and Context Windows

After splitting text, the tokenizer maps each token to an integer ID. The model processes a sequence of IDs subject to a context window, which is the maximum amount of input and generated content it can consider in one request.

```text
Prompt tokens + reserved output tokens <= model context window
```

Long prompts reduce the space available for the answer. Context limits also affect cost and latency because more tokens require more processing.

## Tokenization and Cost

Many hosted models price usage by input and output tokens. Token count varies with:

- Language and writing system
- Whitespace and punctuation
- Source code and markup
- Long or uncommon words
- Repeated instructions and pasted context

Do not estimate cost using word count alone. Use the tokenizer or provider usage information for the model you are actually calling.

## Effects on AI Applications

- Keep prompts concise without removing necessary context.
- Reserve output capacity when setting context limits.
- Chunk long documents at meaningful boundaries for retrieval.
- Preserve code fences and identifiers when tokenizing source code.
- Test multilingual and unusual input because token efficiency varies.
- Avoid splitting retrieved text in the middle of important structures when possible.

## Special Tokens

Models may use special tokens to mark roles, message boundaries, document separators, padding, or the end of generation. These tokens can affect context length and behavior even when they are not visible in the final text.

## Tokenization Is Not Understanding

Tokenization is a representation step. It does not mean the model understands a token as a complete human concept. A single word can become multiple tokens, and a token can include a leading space or punctuation. The model learns relationships among token sequences through training.

## Related Concepts

- [[Probabilistic and Vectorial nature]] - Convert tokens into vector representations
- [[Temperature and Verbosity]] - Generation and output limits
- [[Prompt Engineering Basics]] - Manage context efficiently
- [[REST API]] - APIs often expose token usage and limits
