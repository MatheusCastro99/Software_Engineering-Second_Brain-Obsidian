---
tags:
	- ai-fundamentals
	- neural-networks
	- transformers
category: AI Fundamentals
related: Context Window and Attention, Probabilistic and Vectorial nature, Word Tokenization
---

# Neural Networks and Transformers

A neural network is a model made of connected mathematical operations whose parameters are learned from examples. During training, the model adjusts those parameters to reduce a defined error or loss. During inference, it uses the learned parameters to produce predictions or generated output for new input.

## Neural Network Building Blocks

- **Input** - Numerical representation of data, such as token IDs or embeddings.
- **Weights** - Learned values that control how information is transformed.
- **Layer** - A group of transformations applied to the representation.
- **Activation function** - Adds non-linearity so the network can learn complex relationships.
- **Output** - Prediction, class score, embedding, or token distribution.
- **Loss function** - Measures the difference between a prediction and a target during training.

```text
Input -> Layer -> Activation -> Layer -> Output
						 parameters learned during training
```

## Training and Inference

Training uses examples to update model parameters, often through gradient descent and backpropagation. Inference uses fixed learned parameters to process a new request. Training is generally expensive and performed separately from ordinary application requests.

The model's output is shaped by both learned parameters and the current input context. A capable model can still make errors when the input is ambiguous, outside its learned patterns, or missing important evidence.

## Transformer Architecture

Transformers process sequences using attention rather than relying only on sequential recurrence. This allows the model to relate tokens at different positions and process many tokens in parallel during training.

Major components include:

- Token embeddings and positional information
- Self-attention layers
- Feed-forward layers
- Residual connections
- Normalization layers
- Output projection over the vocabulary

## Self-Attention

For each token, attention compares a query with keys from other tokens and combines their values. A simplified scaled dot-product attention equation is:

$$
\operatorname{Attention}(Q,K,V) = \operatorname{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

This lets the representation of a token incorporate relevant information from other parts of the sequence.

## Language Models

An autoregressive language model predicts the next token based on previous tokens. It repeats this process to generate a sequence. Other transformer designs may encode input for classification, retrieve representations, or transform one sequence into another.

## Strengths and Limitations

Transformers are effective at learning relationships across long sequences and can be adapted to text, code, images, audio, and multimodal tasks. Their limitations include computational cost, context limits, sensitivity to data quality, and the possibility of fluent but incorrect output.

## Practical Implications

- Use token counts and context limits when designing prompts.
- Provide relevant evidence for current or private information.
- Validate model output before executing code or changing state.
- Choose a smaller model when latency, cost, or privacy matters.
- Evaluate models on representative tasks rather than general impressions.

## Related Concepts

- [[Context Window and Attention]] - How models use relationships within context
- [[Probabilistic and Vectorial nature]] - Vectors and token probabilities
- [[Word Tokenization]] - Convert text into model input units
- [[Temperature and Verbosity]] - Control generation behavior
