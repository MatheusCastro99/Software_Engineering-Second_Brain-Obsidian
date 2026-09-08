---
tags:
	- shipping-solutions
	- azure
	- cloud
category: Shipping Solutions
related: Kubernetes, Docker Basics, DevOps, CI-CD Pipeline
---

# Azure Cloud

Microsoft Azure is a cloud platform that provides computing, storage, networking, databases, identity, monitoring, security, and managed application services. Instead of purchasing and maintaining all infrastructure directly, teams provision resources through a portal, command line, APIs, or infrastructure-as-code tools.

## Cloud Service Models

| Model | Customer manages | Azure manages |
|-------|------------------|---------------|
| IaaS | Operating system, runtime, application, data | Physical infrastructure and virtualization |
| PaaS | Application and data | Servers, operating system, runtime, and platform |
| SaaS | Configuration and usage | Most of the application and infrastructure |

Azure App Service is an example of a managed platform service. Azure Virtual Machines provide more infrastructure control but require more operational responsibility.

## Core Azure Resources

- **Resource group** - Logical container for related resources and their lifecycle.
- **Subscription** - Billing, quota, and access boundary.
- **Region** - Geographic Azure location where resources run.
- **Virtual network** - Private network boundary for connected resources.
- **Storage account** - Blob, file, queue, and table storage services.
- **Managed identity** - Azure-managed identity for accessing other resources without embedding credentials.
- **Azure Monitor** - Metrics, logs, alerts, and application insights.

Resources should use consistent names, tags, ownership metadata, and environment labels so they can be discovered and managed safely.

## Common Compute Options

| Service | Best for |
|---------|----------|
| Virtual Machines | Full operating-system control and legacy workloads |
| App Service | Managed web applications and APIs |
| Azure Functions | Event-driven, short-running serverless code |
| Container Apps | Managed containerized applications with scaling |
| Azure Kubernetes Service | Kubernetes workloads requiring cluster capabilities |
| Container Instances | Simple, short-lived containers without cluster management |

Choose the least complex service that satisfies scaling, networking, runtime, and operational requirements.

## Identity and Security

Microsoft Entra ID provides identity and access management. Use role-based access control to grant the minimum permissions required, managed identities for service-to-service access, network restrictions for private resources, and a secret manager such as Azure Key Vault for sensitive values.

Never store passwords, tokens, or connection strings in source control, container images, or pipeline YAML.

## Reliability and Cost

Plan for availability zones, backups, disaster recovery, health checks, and regional failure according to the application's requirements. Cloud resources are not automatically reliable or inexpensive; unused instances, excessive logging, oversized databases, and unbounded storage can create significant cost.

Useful practices include budgets, cost alerts, autoscaling limits, resource tags, right-sizing, and reviewing the monthly cost analysis.

## Deployment Workflow

```text
Code -> Build and test -> Create artifact -> Provision/update infrastructure
		 -> Deploy -> Verify health -> Monitor -> Improve
```

Use [[CI-CD Pipeline]] and infrastructure as code to make deployments repeatable. Keep production approvals and rollback procedures explicit.

## Related Concepts

- [[Kubernetes]] - Container orchestration in Azure and elsewhere
- [[Docker Basics]] - Package applications as containers
- [[DevOps]] - Delivery, operations, and feedback practices
- [[CI-CD Pipeline]] - Automate Azure deployments
- [[Cache and Redis]] - Managed or self-hosted caching workloads
