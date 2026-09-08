---
tags:
	- ai-development
	- github
	- project-memory
category: AI Development Strategies
related: Making use of GitHub, Agents, Sub-Agents, and Multi-Agents Orchestration, Git Fundamentals
---

# GitHub Repo and Issues as a Memory Source

GitHub can provide durable, shared memory for AI-assisted development. Issues capture intent and decisions, pull requests capture implementation and review, and commits provide a traceable history of changes. This memory is more useful than relying on an agent's temporary conversation context.

## What to Store

| GitHub artifact | Useful memory |
|-----------------|---------------|
| Issue | Problem, scope, acceptance criteria, open questions |
| Comment | Decision, investigation result, or clarification |
| Pull request | Proposed implementation, review discussion, validation evidence |
| Commit | Small, attributable change with a clear reason |
| Labels and milestones | Priority, area, status, and release grouping |

## Issue as a Task Contract

A good issue gives an agent enough context to act without guessing:

```markdown
## Problem
Describe the behavior that is wrong or missing.

## Scope
- Files or component likely involved
- Behavior that must remain unchanged

## Acceptance criteria
- [ ] Expected behavior is implemented
- [ ] Focused tests pass
- [ ] Documentation is updated when needed

## Open questions
- Record decisions that still require human input.
```

The issue should describe the desired behavior, not prescribe an implementation unless the design is already decided.

## Pull Requests as Review Memory

A pull request should explain what changed, why it changed, how it was verified, and what remains uncertain. Review comments preserve reasoning that would otherwise disappear after the task is merged.

For agent-created pull requests, require:

- A link to the source issue
- A concise summary of changed behavior
- Tests or commands that were run
- Known limitations and follow-up work
- A clear indication of whether human approval is required

## Revision and Development Loops

```text
Issue -> Plan -> Implement -> Test -> Pull request -> Review -> Revise -> Merge
```

Each loop should produce an artifact. For example, a failed test becomes a comment, a review request becomes a commit, and a final decision becomes part of the issue or pull request description.

## Using GitHub with Agents

1. Create or select one issue for the task.
2. Ask the planning agent to clarify scope and acceptance criteria.
3. Assign implementation work to an agent with limited repository access.
4. Require focused validation before opening a pull request.
5. Use an independent reviewer agent or human reviewer to challenge the result.
6. Update the issue with the outcome and follow-up work.

Avoid opening many issues for one tightly coupled change. Fragmented memory makes it harder for agents and humans to reconstruct the actual decision path.

## Best Practices

- Write issues so they remain understandable without chat history.
- Keep commits small and explain the motivation in the message.
- Link issues, pull requests, and commits.
- Treat labels as searchable metadata, not as a substitute for context.
- Close stale or superseded work explicitly with a reason.
- Never store secrets, tokens, or private customer data in issue text.

## Related Concepts

- [[Making use of GitHub]] - Use GitHub tools in agent workflows
- [[Agents, Sub-Agents, and Multi-Agents Orchestration]] - Coordinate contributors
- [[Git Fundamentals]] - Version control concepts
- [[MCP's]] - Connect agents to GitHub and other systems
