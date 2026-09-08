---
tags:
	- ai-fundamentals
	- prompting
	- llm
category: AI Fundamentals
related: Temperature and Verbosity, Word Tokenization, Probabilistic and Vectorial nature
---

# Prompt Engineering Basics

Prompt engineering is the practice of designing instructions and context so an AI model can produce a useful, accurate, and appropriately structured response. A good prompt reduces ambiguity and makes success observable.

## Anatomy of a Prompt

```text
Role or perspective
Task and objective
Relevant context
Constraints and exclusions
Examples, when useful
Output format
Evaluation criteria
```

Not every prompt needs every component. Include the information that changes the answer and remove irrelevant instructions that compete for attention.

## Basic Template

```text
You are [role or domain perspective].

Task:
[Describe the exact outcome required]

Context:
[Provide the facts, data, code, or audience]

Constraints:
- [Required behavior]
- [Things to avoid]

Output:
[Specify headings, schema, length, or format]

Before finalizing, check that [acceptance criteria].
```

## Clear Instructions

Prefer specific verbs and measurable outcomes:

```text
Weak:  Explain APIs.
Strong: Compare REST and GraphQL for a small .NET service in a table with
				use cases, tradeoffs, and one example request for each.
```

State the audience, scope, assumptions, and definition of done. If a requirement is important, make it explicit rather than expecting the model to infer it.

## Few-Shot Examples

Examples show the model the desired transformation, tone, or structure. They are useful when the task has a format that is difficult to describe in words.

```text
Input: "The server is slow because the database is queried repeatedly."
Output: {"category":"performance", "priority":"high"}

Input: "The button does not respond to keyboard input."
Output: {"category":"accessibility", "priority":"medium"}
```

Examples should be representative and consistent. A misleading example can teach the wrong rule more strongly than a paragraph of instructions can correct it.

## Ask for Structured Output

When another program will consume the response, define a schema:

```json
{
	"summary": "string",
	"risks": ["string"],
	"recommended_action": "string"
}
```

Structured output reduces ambiguity, but the receiving application must still validate required fields, types, allowed values, and safety constraints.

## Grounding and Verification

For tasks that depend on private, current, or precise information:

- Provide the relevant source material or use retrieval.
- Ask the model to distinguish facts from assumptions.
- Request citations or references when appropriate.
- Break complex work into stages.
- Verify important claims with authoritative sources or tests.

Prompting alone cannot guarantee factual accuracy. Better instructions improve behavior, but external evidence and validation remain necessary.

## Iterative Prompt Improvement

1. Write the shortest prompt that expresses the goal.
2. Test it against representative inputs.
3. Record failure cases and ambiguous outputs.
4. Add only the instruction or example that addresses the failure.
5. Re-test normal, edge, and adversarial inputs.

Avoid adding long instructions merely because an earlier output was bad once. Measure whether the change improves the full evaluation set.

## Common Mistakes

- Asking for several unrelated tasks in one unclear paragraph
- Omitting the desired output format
- Providing contradictory priorities
- Including sensitive data unnecessarily
- Treating confident language as evidence
- Using role-play to bypass security or policy constraints
- Relying on a prompt instead of application-level validation

## Related Concepts

- [[Temperature and Verbosity]] - Tune response randomness and length
- [[Word Tokenization]] - Understand input and output limits
- [[Probabilistic and Vectorial nature]] - Why prompts influence likely continuations
- [[Skills]] - Package repeatable prompting workflows
