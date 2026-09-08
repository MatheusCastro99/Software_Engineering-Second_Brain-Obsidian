---
tags:
	- development-lifecycle
	- agile
	- project-management
category: Development Lifecycle
related: Sprints, SDLC, DevOps, CI-CD Pipeline
---

# Agile Methodology

Agile is an approach to software development that delivers valuable working software in short cycles, gathers feedback frequently, and adapts plans as the product and its requirements become clearer. Agile values collaboration and learning over rigid long-term prediction.

## Core Ideas

- Deliver working software frequently.
- Welcome changing requirements when they improve the product.
- Collaborate continuously with customers and stakeholders.
- Keep development and business teams aligned.
- Prefer direct communication and visible work.
- Improve the process through regular reflection.

Agile does not mean working without planning or documentation. It means planning at the level of detail justified by current knowledge and revising the plan as evidence changes.

## Iterative and Incremental Development

Agile work is both iterative and incremental:

- **Iterative** - The team revisits understanding, design, and implementation based on feedback.
- **Incremental** - Each cycle adds a usable piece of product capability.

```text
Plan -> Build -> Test -> Demonstrate -> Learn -> Adjust
```

Fast iterations divided into [[Sprints]] reduce the time between an idea and evidence about whether it works.

## Scrum Roles and Events

Scrum is one framework commonly used to apply Agile principles.

| Element | Responsibility |
|---------|----------------|
| Product Owner | Prioritizes value and clarifies product goals |
| Scrum Master | Supports the process and removes impediments |
| Developers | Build, test, and deliver the increment |
| Product Backlog | Ordered list of product work |
| Sprint Backlog | Work selected for the current sprint |
| Increment | Usable result produced during the sprint |

Common events include sprint planning, daily coordination, sprint review, and retrospective.

## User Stories and Acceptance Criteria

User stories express value from a user's perspective:

```text
As a customer, I want to filter products by price
so that I can find items within my budget.
```

Acceptance criteria make the expected behavior testable:

- The user can enter a minimum and maximum price.
- Results outside the range are excluded.
- Invalid ranges produce a clear validation message.

## Definition of Done

The Definition of Done is a shared quality threshold. It may include completed implementation, code review, automated tests, documentation, accessibility checks, and successful deployment to the agreed environment.

## Common Misunderstandings

- Agile is not an excuse to skip architecture or quality.
- Daily meetings are not the definition of Agile.
- A sprint is not successful if it produces unfinished work with no usable outcome.
- Velocity is a planning signal, not a productivity score.
- Changing priorities does not mean changing the goal every hour.

## Best Practices

- Keep work small enough to complete and validate in one cycle.
- Make priorities and blockers visible.
- Demonstrate working software, not only status reports.
- Reserve time to improve tests, tooling, and technical debt.
- Use retrospectives to change one or two concrete behaviors.

## Related Concepts

- [[Sprints]] - Time-boxed Agile iterations
- [[SDLC]] - The broader software development lifecycle
- [[CI-CD Pipeline]] - Automate feedback and delivery
- [[DevOps]] - Connect development and operations