---
tags:
	- development-lifecycle
	- ci-cd
	- automation
category: Development Lifecycle
related: DevOps, Agile methodology, SDLC, Git Fundamentals
---

# CI/CD Pipeline

CI/CD is a set of practices and automated steps that build, test, package, and deliver software. **Continuous Integration (CI)** frequently integrates small changes and verifies them. **Continuous Delivery** keeps validated changes ready for release. **Continuous Deployment** automatically releases validated changes to production.

## Typical Pipeline

```text
Commit -> Build -> Unit tests -> Static analysis -> Package
			 -> Integration tests -> Security checks -> Deploy -> Monitor
```

Each stage should provide fast, useful feedback and stop the pipeline when a required quality gate fails.

## Continuous Integration

CI reduces integration risk by requiring developers to merge or validate small changes frequently. A CI pipeline commonly:

- Restores dependencies
- Compiles the application
- Runs unit and integration tests
- Performs linting and static analysis
- Publishes test and coverage results
- Creates a build artifact

The build should be reproducible from a clean environment and should not depend on an individual developer's machine.

## Delivery vs. Deployment

| Practice | Meaning |
|----------|---------|
| Continuous delivery | Every approved change is deployable, but release may require approval |
| Continuous deployment | Every change that passes the gates is released automatically |
| Manual release | A person chooses when an already-built artifact is released |

Separating build from release makes it possible to promote the same artifact through development, staging, and production without rebuilding it differently at each stage.

## Pipeline Stages

### Build and Test

Compile the code and run the fastest reliable tests first. Fail early on syntax, type, formatting, or unit-test errors.

### Quality and Security

Check dependencies, secrets, licenses, code quality, container images, and common vulnerabilities. Security scanning complements, but does not replace, secure design and review.

### Package

Create a versioned artifact such as a container image, application bundle, or deployment package. Record the commit and build metadata so the artifact can be traced back to source.

### Deploy and Verify

Deploy to an environment and run smoke tests, health checks, and relevant integration tests. Monitor the release and define rollback or roll-forward procedures.

## Deployment Strategies

- **Rolling deployment** - Replace instances gradually.
- **Blue-green deployment** - Maintain old and new environments and switch traffic.
- **Canary deployment** - Send a small percentage of traffic to the new version first.
- **Feature flags** - Deploy code while controlling feature exposure separately.

## Pipeline Best Practices

- Keep pipeline configuration versioned with the application.
- Make stages repeatable and as independent as practical.
- Cache dependencies carefully without hiding stale results.
- Store secrets in a secure secret manager, never in source control.
- Keep feedback fast and publish clear failure logs.
- Use approval gates for high-risk production changes.
- Measure lead time, deployment frequency, change failure rate, and recovery time.

## Related Concepts

- [[DevOps]] - Culture and practices around delivery and operations
- [[Agile methodology]] - Short feedback cycles and incremental delivery
- [[SDLC]] - Where CI/CD fits in the lifecycle
- [[Git Fundamentals]] - Source control triggers and history