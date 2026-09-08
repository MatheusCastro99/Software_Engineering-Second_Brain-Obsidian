---
tags:
	- development-lifecycle
	- technical-debt
	- maintainability
category: Development Lifecycle
related: Agile methodology, SDLC, Release Management, SOLID Principles
---

# Technical Debt

Technical debt is the future cost created when a team chooses a quick, incomplete, or fragile solution instead of a more maintainable one. Some debt is deliberate and strategic; some is accidental and discovered later. Like financial debt, it may be useful when managed, but it creates interest through slower delivery, defects, and higher risk.

## Common Sources

- Missing or weak automated tests
- Duplicated or tightly coupled code
- Outdated dependencies and frameworks
- Temporary workarounds that became permanent
- Poor database or API design
- Inconsistent documentation and runbooks
- Manual deployment and environment configuration
- Unclear ownership of important components

## Types of Debt

| Type | Example | Consequence |
|------|---------|-------------|
| Code debt | Complex method or duplication | Slower changes and more defects |
| Design debt | Inflexible architecture | Difficult feature work and scaling |
| Test debt | Missing regression coverage | Fear of changing behavior |
| Infrastructure debt | Manual or outdated environments | Slow and unreliable releases |
| Documentation debt | Missing operational knowledge | Onboarding and incident delays |
| Dependency debt | Unsupported package versions | Security and compatibility risk |

## Principal and Interest

- **Principal** is the work required to improve or replace the current solution.
- **Interest** is the repeated cost paid while the debt remains, such as extra debugging, slower reviews, or duplicated effort.

A small shortcut may have low interest if it is isolated and documented. A shortcut in a central system can accumulate interest across every future change.

## Identifying and Prioritizing Debt

Record debt where it is visible, such as an issue, code comment with an owner, architecture decision record, or backlog item. Prioritize using:

```text
Priority = impact x frequency x risk x cost of delay
```

High-priority debt often affects security, data integrity, release reliability, or a frequently changed area. Not all old or imperfect code needs to be rewritten.

## Paying Down Debt

- Refactor while changing a component, when the scope is controlled.
- Add characterization tests before changing risky behavior.
- Replace manual steps with automation.
- Upgrade dependencies on a regular schedule.
- Simplify interfaces and remove unused code.
- Reserve capacity for maintenance in planning.
- Measure whether the change actually reduces future effort.

Avoid large rewrites based only on discomfort with existing code. Define the problem, preserve behavior with tests, and migrate incrementally when possible.

## Debt and Agile Planning

Technical debt should be visible alongside feature work. It can be represented as backlog items, acceptance criteria, maintenance tasks, or an explicit quality objective within a [[Sprints|sprint]]. Hiding debt until it becomes an incident makes prioritization harder and increases its cost.

## Related Concepts

- [[Agile methodology]] - Make maintenance visible during planning
- [[SDLC]] - Manage quality throughout the lifecycle
- [[Release Management]] - Reduce release risk
- [[SOLID Principles]] - Design practices that reduce code debt
- [[CI-CD Pipeline]] - Automated checks that prevent new debt
