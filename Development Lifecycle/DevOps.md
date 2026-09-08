---
tags:
	- development-lifecycle
	- devops
	- automation
category: Development Lifecycle
related: CI-CD Pipeline, Agile methodology, SDLC, Azure Cloud
---

# DevOps

DevOps is a set of cultural practices, technical practices, and automation that brings software development and IT operations closer together. Its goal is to deliver reliable changes quickly while sharing responsibility for the system across its lifecycle.

## Core Principles

- **Collaboration** - Development, operations, security, and product teams work toward shared outcomes.
- **Automation** - Repetitive build, test, deployment, and infrastructure tasks are automated.
- **Continuous feedback** - Telemetry, incidents, tests, and user feedback guide improvements.
- **Shared ownership** - Teams remain responsible for software after it is deployed.
- **Small changes** - Smaller releases are easier to understand, review, and recover.

DevOps is broader than a tool such as Azure DevOps. Azure DevOps can provide boards, repositories, pipelines, test tools, and package feeds, but the practices still depend on team behavior and engineering discipline.

## DevOps Lifecycle

```text
Plan -> Code -> Build -> Test -> Release -> Deploy -> Operate -> Monitor
	^                                                        |
	+---------------------- Feedback ------------------------+
```

This loop connects planning and development with production operation. Monitoring is not the final step; it supplies information for the next planning and improvement cycle.

## Azure DevOps Pipelines

Azure DevOps Pipelines can automate CI/CD workflows for applications and infrastructure. A pipeline may be defined in YAML so its stages, variables, approvals, and dependencies are reviewed alongside the code.

```yaml
trigger:
	- main

steps:
	- script: dotnet restore
	- script: dotnet build --no-restore
	- script: dotnet test --no-build
```

Production workflows usually add artifact publishing, environment approvals, deployment steps, health checks, and rollback handling.

## Infrastructure and Configuration

Infrastructure as Code describes environments in versioned, repeatable definitions. Configuration should be separated from application code, while secrets should be supplied through a secure secret store and protected pipeline variables.

## Observability

Observability helps teams understand system behavior through:

- **Logs** - Detailed events and diagnostic context
- **Metrics** - Numeric measurements such as latency and error rate
- **Traces** - A request's path across services
- **Alerts** - Signals that require investigation or action

Useful telemetry includes correlation IDs, deployment versions, dependency failures, and user-impact indicators. Avoid logging credentials, tokens, or sensitive personal data.

## Reliability and Incident Response

DevOps includes the ability to recover when changes fail. Teams should define health checks, rollback or roll-forward procedures, incident ownership, escalation paths, and blameless post-incident learning. A post-incident review should improve systems and processes rather than focus on punishment.

## Best Practices

- Automate a safe path from commit to deployment.
- Keep environments as consistent as possible.
- Use least privilege for pipeline identities.
- Review infrastructure and pipeline changes like application code.
- Deploy small changes and monitor their impact.
- Treat security as part of every stage, not a final inspection.

## Related Concepts

- [[CI-CD Pipeline]] - Automated integration and delivery
- [[Agile methodology]] - Iterative planning and feedback
- [[SDLC]] - The complete lifecycle of software
- [[Azure Cloud]] - Cloud services and deployment environment
- [[Docker Basics]] - Consistent application packaging