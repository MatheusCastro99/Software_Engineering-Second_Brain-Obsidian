---
tags:
	- ai-development
	- github
	- mcp
category: AI Development Strategies
related: GitHub Repo and Issues as a Memory source, MCP's, Skills
---

# Making Use of GitHub

GitHub can act as the coordination surface for AI-assisted development. Agents can read issues, inspect repository history, open pull requests, respond to review feedback, and record decisions through GitHub tools exposed by an MCP server.

## Practical Uses

- Create issues for complex tasks and acceptance criteria.
- Search existing issues before starting duplicate work.
- Assign independent investigation to temporary agents.
- Open pull requests so changes receive a separate review.
- Use labels and milestones to prioritize work.
- Close or release unnecessary agents when their task is complete.

## Issue-Driven Agent Workflow

```text
1. Read the issue and linked history
2. Clarify scope and acceptance criteria
3. Create a short implementation plan
4. Delegate independent research or review
5. Implement and run focused checks
6. Open or update a pull request
7. Record review decisions and close the issue
```

The issue is the durable task record. The agent conversation is temporary working context and should not be the only place where requirements or decisions exist.

## Releasing Unnecessary Agents

Every active agent adds cost and can introduce conflicting edits or stale assumptions. Stop a sub-agent when it has returned its findings, when the question is answered, or when its work is no longer relevant. Record useful output in the issue or pull request before releasing it.

## GitHub Tool Permissions

Separate read and write capabilities where possible:

| Access | Examples |
|--------|----------|
| Read-only | Search issues, inspect files, read pull requests |
| Review | Comment, request changes, approve |
| Write | Create branches, commits, issues, or pull requests |
| Administrative | Change settings, permissions, or branch protection |

An agent that only needs to investigate should not receive write access. Destructive or externally visible actions should require explicit approval.

## Useful Issue Comment Format

```markdown
### Investigation result
The failure occurs when the request contains an empty identifier.

### Evidence
- Reproduced by: `dotnet test --filter FullyQualifiedName~RequestTests`
- Affected code: request validation boundary

### Recommendation
Reject the request before the service call and add a focused regression test.
```

This format makes comments useful to later agents and human reviewers without requiring the original conversation.

## Best Practices

- Link every pull request to an issue.
- Search before creating new tracking work.
- Keep status updates factual and evidence-based.
- Use pull requests as the review boundary for non-trivial changes.
- Remove access and stop agents when their work ends.
- Keep secrets out of issues, comments, logs, and prompts.

## Related Concepts

- [[GitHub Repo and Issues as a Memory source]] - GitHub as durable project memory
- [[MCP's]] - Tool connectivity and permissions
- [[Single and Multi Thread Workflows]] - Parallel task management