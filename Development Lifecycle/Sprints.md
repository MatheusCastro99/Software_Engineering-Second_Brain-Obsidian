---
tags:
	- development-lifecycle
	- agile
	- sprints
category: Development Lifecycle
related: Agile methodology, SDLC, CI-CD Pipeline
---

# Sprints

A sprint is a fixed-length period in which a team works toward a defined goal and produces a usable increment of software. Sprints create a regular feedback rhythm without implying that every task or requirement is known in advance.

## Sprint Structure

```text
Product goal -> Sprint planning -> Daily coordination
						 -> Build and test -> Review -> Retrospective
```

The team selects a realistic amount of high-priority work, protects the sprint goal from unnecessary disruption, and inspects the result at the end.

## Sprint Events

### Sprint Planning

The team discusses the goal, available capacity, priorities, dependencies, risks, and acceptance criteria. Selected work becomes the sprint backlog. The sprint goal explains the outcome more clearly than a list of disconnected tasks.

### Daily Coordination

The team briefly synchronizes on progress, next steps, and impediments. It is a coordination activity, not a manager's status interrogation or a requirement for every person to give the same scripted report.

### Sprint Review

The team demonstrates the increment to stakeholders, gathers feedback, and updates product priorities. A review should show working behavior rather than only slides or completed task counts.

### Sprint Retrospective

The team examines how it worked and selects concrete improvements. Useful discussion areas include collaboration, quality, tooling, interruptions, estimation, and technical debt.

## Sprint Backlog

Break selected work into tasks that are small enough to track and test. Each item should have a clear outcome and acceptance criteria.

```text
Story: As a user, I can reset my password.

Tasks:
- Design the reset request and response
- Implement token creation and expiration
- Build the reset form
- Add success, invalid-token, and expired-token tests
```

The team may refine or split tasks during the sprint as it learns more, while keeping the sprint goal stable.

## Estimation and Capacity

Estimates express relative effort, uncertainty, and complexity; they are not promises of exact hours. Capacity accounts for meetings, support work, holidays, interruptions, and unfinished work carried over from earlier cycles.

Velocity can help a team forecast based on its own history, but comparing velocity between teams or using it as an individual performance score creates unhealthy incentives.

## Definition of Done

An item is done only when it meets the shared quality standard. This may include implementation, code review, automated tests, security checks, documentation, accessibility review, and deployment to the agreed environment.

## Common Sprint Risks

- Starting more work than the team can finish
- Accepting vague stories without testable outcomes
- Treating unfinished work as complete
- Allowing interruptions to replace planned priorities
- Deferring testing until the final day
- Measuring activity instead of delivered value

## Best Practices

- Set one understandable sprint goal.
- Limit work in progress and finish before starting more.
- Surface blockers early.
- Integrate and test continuously through the sprint.
- Reserve capacity for maintenance and urgent support.
- Use the retrospective to make small, measurable changes.

## Related Concepts

- [[Agile methodology]] - Principles behind iterative work
- [[SDLC]] - Sprints as repeated lifecycle cycles
- [[CI-CD Pipeline]] - Continuous validation during a sprint
- [[DevOps]] - Deploying and operating the increment
