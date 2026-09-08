---
tags:
	- ai-development
	- mcp
	- tools
category: AI Development Strategies
related: Agentic Architecture, Skills, Making use of GitHub
---

# Model Context Protocol (MCP)

Model Context Protocol (MCP) is a standard way for AI applications to discover and use external tools, resources, and prompt templates. It separates an agent from the implementation details of a service such as GitHub, a database, a filesystem, or an internal API.

## Core Concepts

- **Host** - The AI application that manages the conversation and permissions.
- **Client** - The protocol connection created by the host.
- **Server** - A process that exposes capabilities to the client.
- **Tool** - An operation that can be invoked, often with structured input.
- **Resource** - Data that can be read as context.
- **Prompt** - A reusable prompt template supplied by a server.

## Request Flow

```text
User request -> Host -> MCP client -> MCP server -> External system
																					 |
																					 v
																	Structured result -> Agent context
```

The server owns the integration logic, while the host decides which servers and capabilities are available. This makes tools reusable across compatible AI applications.

## Example Capabilities

An MCP server might expose:

| Capability | Example |
|------------|---------|
| Tool | Search GitHub issues or create a pull request |
| Resource | Read a project specification or database schema |
| Prompt | Generate a standard code-review request |

## Safe Tool Design

Good tools have narrow responsibilities, descriptive names, explicit input schemas, predictable output, and clear side effects. A tool called `update_repository` is difficult to reason about; separate operations such as `create_issue`, `read_file`, and `run_tests` are easier to authorize and audit.

Before calling a tool, an agent should know:

- What data it reads or changes
- Whether the operation is reversible
- Which identity and permissions it uses
- What errors can be returned
- What confirmation is required

## MCP in Agentic Development

MCP can connect an agent to the systems it needs during a development workflow:

1. Read a GitHub issue as the task contract.
2. Inspect repository files and history.
3. Run a focused test or build command.
4. Create a review artifact such as a comment or pull request.

The protocol supplies access, but it does not replace authorization, input validation, or human review.

## Risks and Guardrails

- Install servers only from trusted sources.
- Give each server the minimum credentials it needs.
- Separate read-only and write-capable connections.
- Review tool descriptions because they influence agent behavior.
- Log important calls without exposing secrets.
- Validate tool results before using them in a later action.
- Require confirmation for destructive or externally visible operations.

## MCP vs. Skills

An MCP server provides access to an external capability. A skill provides instructions for using a capability consistently. For example, an MCP server may expose GitHub issue operations, while a skill defines how to write an issue with clear acceptance criteria.

## Related Concepts

- [[Agentic Architecture]] - Tool use inside an agent loop
- [[Skills]] - Reusable behavior and instructions
- [[Making use of GitHub]] - A practical MCP-backed workflow
- [[Error Handling]] - Handle failed tool calls
