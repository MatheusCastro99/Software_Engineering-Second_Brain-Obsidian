---
tags:
	- development-lifecycle
	- release-management
	- deployment
category: Development Lifecycle
related: CI-CD Pipeline, DevOps, SDLC, Technical Debt
---

# Release Management

Release management is the process of planning, coordinating, validating, deploying, and monitoring a software release. It connects completed development work with a controlled change in a target environment.

## Release Flow

```text
Plan scope -> Build artifact -> Validate -> Approve -> Deploy
					 -> Monitor -> Communicate -> Learn and improve
```

The release artifact should be traceable to a source commit and should be promoted through environments without being rebuilt differently for each one.

## Release Planning

Define the release scope, target environment, dependencies, owners, risks, rollout timing, communication plan, and success criteria. Confirm that unfinished work is excluded or protected behind a feature flag.

## Release Readiness Checklist

- Acceptance criteria and critical tests pass.
- Security, dependency, and migration checks are complete.
- Configuration and secrets exist in the target environment.
- Monitoring, alerts, and health checks are ready.
- Backups and rollback or roll-forward plans are tested.
- Support teams and stakeholders know what is changing.
- The release version and deployment notes are recorded.

## Deployment Strategies

| Strategy | Description | Main benefit |
|----------|-------------|--------------|
| Big bang | Deploy to all targets at once | Simple process, larger blast radius |
| Rolling | Replace instances gradually | Reduced interruption |
| Blue-green | Switch traffic between two environments | Fast rollback by switching back |
| Canary | Expose a small audience first | Early evidence with limited impact |
| Feature flag | Deploy code separately from exposure | Gradual activation and quick disable |

Choose the strategy according to risk, architecture, traffic, database compatibility, and rollback capability.

## Database and Configuration Changes

Database changes can outlive application versions, so migrations should be backward-compatible during a transition when rolling or blue-green deployments are used. Prefer expand-and-contract changes: add compatible structures, migrate or dual-write data, switch readers, and remove obsolete structures later.

Configuration should be externalized from the artifact. Secrets belong in a secure secret manager, not in release notes, source control, or container images.

## Rollback and Recovery

A rollback restores a previous known-good version. A roll-forward fixes the current version with a new release. Neither is sufficient if a database migration or data mutation cannot be reversed, so recovery plans must include data behavior and not only application binaries.

## Monitoring After Release

Watch error rates, latency, availability, resource usage, business metrics, logs, and user reports. Compare the release with a known baseline and define the threshold that triggers pausing, rollback, or investigation.

## Release Notes

Useful release notes include:

- Version and deployment date
- User-visible changes
- Fixed defects and known limitations
- Migration or configuration steps
- Compatibility or breaking changes
- Rollback instructions
- Links to the relevant issue, build, and artifact

## Related Concepts

- [[CI-CD Pipeline]] - Automate validation and deployment
- [[DevOps]] - Operate and learn from releases
- [[SDLC]] - Release as part of the full lifecycle
- [[Technical Debt]] - Reduce accumulated release risk
- [[Azure Cloud]] - Cloud deployment environments
