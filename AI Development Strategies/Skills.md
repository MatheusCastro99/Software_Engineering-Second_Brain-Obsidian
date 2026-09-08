---
tags:
	- ai-development
	- skills
	- agents
category: AI Development Strategies
related: Agentic Architecture, MCP's, Agents, Sub-Agents, and Multi-Agents Orchestration
---

# Skills

An AI skill is a reusable package of instructions, decision rules, examples, and workflow constraints that helps an agent perform a recurring task consistently. A skill is behavior guidance; it is not the same as a model, a tool, or an MCP server.

## Skill Components

- **Purpose** - The task the skill supports
- **Inputs** - Information the agent must receive
- **Procedure** - Ordered steps and decision points
- **Constraints** - Rules, permissions, and scope limits
- **Output** - Expected format and required evidence
- **Validation** - Checks that determine whether the result is complete

## Skill vs. Tool vs. Agent

| Concept | Role |
|---------|------|
| Skill | Teaches an agent how to approach a task |
| Tool | Performs an operation such as reading a file or running a test |
| Agent | Uses a model, context, skills, and tools to pursue a goal |
| MCP server | Exposes tools or resources through a standard protocol |

A code-review skill may instruct an agent to inspect the diff, prioritize bugs, cite files, and identify test gaps. It does not itself run the tests; a tool does that.

## Example Skill Structure

```markdown
# Review a Pull Request

## Purpose
Find behavioral regressions and missing tests.

## Steps
1. Read the pull request description and acceptance criteria.
2. Inspect the changed files and nearby call sites.
3. Run the narrowest relevant checks.
4. Report findings ordered by severity.

## Constraints
- Do not modify files during review.
- Do not report style preferences as bugs.

## Output
Include file references, impact, evidence, and remaining test gaps.
```

## Designing Effective Skills

- State when the skill should and should not be used.
- Define the smallest useful workflow.
- Prefer local repository conventions over generic advice.
- Include failure handling and escalation conditions.
- Specify what evidence the agent must return.
- Keep instructions concise enough to remain in working context.
- Version or review skills when their behavior affects production work.

## Skill Lifecycle

```text
Identify repetition -> Write the workflow -> Test on examples -> Review failures -> Refine -> Reuse
```

Create a skill after a pattern has proved reusable. A skill that tries to cover every possible task becomes difficult to follow and can conflict with more specific instructions.

## Common Failure Modes

- **Vague goal** - The agent cannot tell when the task is complete.
- **Conflicting instructions** - The skill disagrees with repository conventions.
- **Missing validation** - The output sounds correct but is not checked.
- **Overloaded skill** - Too many unrelated responsibilities reduce consistency.
- **Hidden assumptions** - Required context or permissions are not stated.

## Related Concepts

- [[Agentic Architecture]] - Skills guide agent behavior inside a loop
- [[MCP's]] - Skills can guide the use of MCP tools
- [[Agents, Sub-Agents, and Multi-Agents Orchestration]] - Assign skills to specialists
- [[Error Handling]] - Define recovery and escalation behavior
