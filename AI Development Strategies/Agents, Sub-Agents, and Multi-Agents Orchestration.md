---
tags:
	- ai-development
	- agents
	- orchestration
category: AI Development Strategies
related: Agentic Architecture, Single and Multi Thread Workflows, Skills
---

# Agents, Sub-Agents, and Multi-Agents Orchestration

Orchestration is the process of coordinating AI agents, tools, context, and verification so a larger task can be completed reliably. A multi-agent design is useful only when dividing the work improves quality, speed, or isolation enough to justify the coordination overhead.

## Terminology

- **Agent** - An AI worker with instructions, context, tools, and a goal.
- **Sub-agent** - A temporary or specialized agent invoked by another agent.
- **Orchestrator** - The controller that assigns work, tracks state, and combines results.
- **Handoff** - A transfer of responsibility and context from one agent to another.
- **Supervisor** - An agent that delegates work and reviews returned results.

## When to Use Multiple Agents

Use multiple agents when tasks have clear boundaries, different expertise requirements, or independent work that can run in parallel. Keep one agent when the task is small, highly coupled, or requires frequent shared context.

| Strategy | Best for | Main cost |
|----------|----------|-----------|
| Single agent | Small, sequential tasks | Limited specialization |
| Supervisor and workers | Delegation and review | More context and coordination |
| Parallel specialists | Independent research or checks | Merging conflicting results |
| Pipeline | Fixed stages such as plan, build, test | Less flexible when a stage changes |

## Orchestration Workflow

```text
Request -> Decompose -> Assign -> Execute -> Validate -> Integrate -> Report
```

Each handoff should include the goal, relevant files or data, constraints, expected output, and completion criteria. Sending only a vague instruction forces the receiving agent to rediscover context and increases inconsistency.

## Example: Feature Development

1. A planning agent converts the request into acceptance criteria.
2. A research agent identifies the local implementation pattern and relevant dependencies.
3. An implementation agent changes the smallest necessary files.
4. A testing agent runs focused checks and adds missing coverage.
5. A review agent checks for regressions, security risks, and scope creep.
6. The supervisor integrates the findings and presents one final result.

The implementation agent should not be the only source of truth about correctness. Independent validation is valuable because it can challenge assumptions made during implementation.

## Shared State and Handoffs

Use a structured handoff rather than copying an entire conversation:

```yaml
task: Add validation for API request payloads
files:
	- src/Api/Requests/CreateUserRequest.cs
constraints:
	- Preserve the public API
	- Follow existing validation conventions
acceptance:
	- Invalid email addresses are rejected
	- Focused tests pass
returned_artifacts:
	- Changed files
	- Test command and result
	- Remaining risks
```

Durable state can live in a repository issue, pull request, test report, or task record. Temporary reasoning should not be treated as durable project memory.

## Guardrails

- Give each agent the minimum permissions it needs.
- Limit the number of delegation and retry steps.
- Require validation before merging or releasing changes.
- Record failures instead of silently retrying forever.
- Make ownership explicit when two agents can edit the same file.
- Use human approval for destructive or externally visible actions.

## Common Failure Modes

- **Duplicate work** - Two agents solve the same task because ownership was unclear.
- **Conflicting edits** - Parallel agents modify the same lines without a merge strategy.
- **Context loss** - A handoff omits constraints or acceptance criteria.
- **Authority confusion** - A specialist makes decisions outside its assignment.
- **Consensus without evidence** - Several agents agree, but none runs a real check.

## Related Concepts

- [[Agentic Architecture]] - The system-level agent loop
- [[Single and Multi Thread Workflows]] - Sequential and parallel execution choices
- [[Skills]] - Reusable capabilities for agents
- [[GitHub Repo and Issues as a Memory source]] - Durable task state
