---
tags:
	- development-lifecycle
	- sdlc
	- software-engineering
category: Development Lifecycle
related: Agile methodology, CI-CD Pipeline, DevOps, Sprints
---

# Software Development Life Cycle (SDLC)

The Software Development Life Cycle (SDLC) is a structured way to plan, build, test, release, operate, and improve software. It provides visibility into the work required to turn a need into a maintainable product.

## Lifecycle Stages

| Stage | Main questions | Typical outputs |
|-------|----------------|-----------------|
| Planning | What problem and constraints exist? | Goals, scope, estimates, risks |
| Requirements | What must the system do? | User stories, acceptance criteria |
| Design | How should it work? | Architecture, data model, interfaces |
| Implementation | How will it be built? | Source code and configuration |
| Testing | Does it work and remain safe? | Test results and defect reports |
| Deployment | How will users receive it? | Release artifact and deployment record |
| Operations | Is it healthy in its environment? | Monitoring, support, incident data |
| Maintenance | How will it evolve? | Fixes, improvements, and new releases |

The stages may overlap and repeat. In [[Agile methodology]], a team moves through a smaller version of this cycle during each [[Sprints|sprint]] rather than waiting until the end of the entire project.

## Requirements and Scope

Requirements describe user needs, business rules, quality attributes, integrations, constraints, and acceptance criteria. A useful requirement is understandable, testable, prioritized, and connected to a user or business outcome.

Uncontrolled scope growth increases risk. Make changes visible, explain their impact, and reprioritize rather than quietly adding work to an active delivery cycle.

## Design and Risk

Design decisions should address architecture, data, security, performance, availability, accessibility, deployment, and observability. Record important decisions and assumptions so future maintainers understand why a solution was chosen.

Risk management can include prototypes, threat modeling, dependency checks, performance tests, and early integration with uncertain systems.

## Testing Across the Lifecycle

- **Unit tests** - Verify small units in isolation.
- **Integration tests** - Verify components working together.
- **End-to-end tests** - Verify important user workflows.
- **Performance tests** - Measure behavior under expected load.
- **Security tests** - Identify weaknesses and incorrect access control.
- **Acceptance tests** - Confirm the delivered behavior meets requirements.

Automated checks in a [[CI-CD Pipeline]] provide rapid feedback, but exploratory testing and human review still contribute important coverage.

## Deployment and Operations

Deployment should be repeatable, observable, and reversible. Define configuration management, database migration behavior, health checks, alert thresholds, rollback procedures, and ownership before a release reaches users.

## Lifecycle Models

| Model | Characteristics |
|-------|-----------------|
| Waterfall | Sequential stages with extensive upfront planning |
| Iterative | Repeated cycles refine the solution |
| Agile | Short increments, frequent feedback, adaptive planning |
| DevOps | Development and operations share delivery and operational responsibility |

No model removes the need for clear goals, quality checks, communication, and risk management.

## Definition of Success

Success is not merely completing tasks or releasing code. A successful lifecycle produces software that solves the intended problem, meets quality and security expectations, can be operated reliably, and can be changed without unreasonable cost.

## Related Concepts

- [[Agile methodology]] - Adaptive development approach
- [[Sprints]] - Time-boxed delivery cycles
- [[CI-CD Pipeline]] - Continuous verification and release
- [[DevOps]] - Operational ownership and feedback
- [[Error Handling]] - Robust software behavior
