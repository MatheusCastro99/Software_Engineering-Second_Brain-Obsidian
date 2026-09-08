---
tags:
	- ai-development
	- agentic-ai
	- architecture
category: AI Development Strategies
related: Agents, Sub-Agents, and Multi-Agents Orchestration, MCP's, Skills
---

# Agentic Architecture

Agentic architecture is a software design approach in which an AI system can interpret a goal, make decisions, use tools, observe results, and continue working until it reaches a defined stopping condition. The model is one component in a controlled system, not the entire application.

## Core Components

| Component | Responsibility |
|-----------|----------------|
| User or event | Supplies the goal, request, or trigger |
| Agent | Plans work and selects the next action |
| Model | Reasons over context and proposes actions |
| Tools | Read data, change state, or call external services |
| Memory | Preserves useful context across steps or sessions |
| Orchestrator | Controls sequencing, retries, permissions, and limits |
| Evaluator | Checks whether the result satisfies requirements |

## The Agent Loop

Most agentic systems follow an observe-plan-act-evaluate cycle:

```text
1. Observe the task, context, and available tool results
2. Plan the next smallest useful action
3. Act by calling a tool or producing an intermediate result
4. Observe the result and update the working context
5. Evaluate progress against the goal
6. Stop, ask for clarification, or continue
```

An explicit loop is safer than allowing an agent to run without boundaries. Useful limits include maximum steps, timeouts, token budgets, allowed tools, and human approval for irreversible actions.

## Workflow Example

For a request to fix a failing API test, an agent might:

1. Read the issue and identify acceptance criteria.
2. Inspect the failing test and the implementation it exercises.
3. Run the narrow test to reproduce the failure.
4. Propose and apply a small code change.
5. Run the same test and related checks.
6. Report the change, evidence, and remaining risks.

The agent should not claim success merely because a code edit was made. The evaluation step must use observable evidence such as tests, compiler output, or a review of the changed behavior.

## Architectural Patterns

### Single Agent

One agent handles planning, tool use, and verification. This is simple to operate and is a good default for bounded tasks.

### Supervisor and Specialists

A supervisor delegates focused tasks to specialist agents, such as research, implementation, testing, and review. Delegation is useful when responsibilities can be separated, but it adds coordination and context-transfer costs.

### Event-Driven Agent

An event, such as a new issue or failed build, starts a bounded workflow. The event payload becomes the initial context and the result is recorded in a durable system such as GitHub Issues.

## Design Principles

- Keep tools narrow, typed, and explicit about side effects.
- Separate planning from permission to perform risky actions.
- Make intermediate state inspectable and resumable.
- Prefer deterministic code for validation, parsing, and business rules.
- Treat model output as untrusted input and validate it at every boundary.
- Define success and stopping conditions before the agent starts.

## Common Failure Modes

- **Runaway loops** - The agent repeats actions without measurable progress.
- **Context drift** - Old assumptions remain in the context after the code changes.
- **Tool overreach** - A broad tool permits changes beyond the requested scope.
- **False completion** - The agent reports success without running a meaningful check.
- **Hidden state** - A later step cannot reproduce why an earlier decision was made.

## Related Concepts

- [[Agents, Sub-Agents, and Multi-Agents Orchestration]] - Coordinate one or more agents
- [[MCP's]] - Standardize access to external tools and data
- [[Skills]] - Package reusable instructions and workflows
- [[Single and Multi Thread Workflows]] - Choose sequential or parallel execution
- [[Error Handling]] - Handle failures in tools and workflows
