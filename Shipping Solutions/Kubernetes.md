---
tags:
	- shipping-solutions
	- kubernetes
	- containers
category: Shipping Solutions
related: Docker Basics, Azure Cloud, DevOps, CI-CD Pipeline
---

# Kubernetes

Kubernetes is an open-source platform for deploying, scaling, networking, and operating containerized applications. It maintains the desired state declared by the operator and works continuously to make the running cluster match that state.

## Core Objects

| Object | Responsibility |
|--------|----------------|
| Cluster | The complete Kubernetes control plane and worker environment |
| Node | Machine or virtual machine that runs workloads |
| Pod | Smallest deployable unit, containing one or more containers |
| Deployment | Manages replicated, replaceable application pods |
| Service | Stable network endpoint for a group of pods |
| ConfigMap | Non-secret configuration data |
| Secret | Sensitive configuration data, with appropriate protection |
| Namespace | Logical isolation and organization within a cluster |
| Ingress | HTTP routing from outside the cluster to services |

## Desired State and Reconciliation

An operator declares what should run, such as three replicas of a web application. Kubernetes controllers compare the desired state with the current state and create, replace, or remove resources as needed.

```text
Manifest -> API server -> Scheduler -> Node and kubelet -> Running pod
		 ^                                                   |
		 +---------------- Reconciliation ------------------+
```

Kubernetes does not make application code automatically correct. It can restart a failed container, but the application still needs health checks, useful logs, correct configuration, and safe data handling.

## Deployment Example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
	name: web-api
spec:
	replicas: 3
	selector:
		matchLabels:
			app: web-api
	template:
		metadata:
			labels:
				app: web-api
		spec:
			containers:
				- name: web-api
					image: example/web-api:1.0.0
					ports:
						- containerPort: 8080
```

Pin image versions instead of relying on a mutable `latest` tag. Add resource requests and limits, readiness probes, liveness probes, and a controlled rollout strategy for production workloads.

## Networking

Pods are replaceable and their IP addresses can change. Services provide stable discovery and load balancing. Ingress or a gateway handles external HTTP routing, TLS termination, and host or path rules.

## Storage and Configuration

Containers should generally be treated as replaceable. Persistent data belongs in a persistent volume or an external managed data service. Keep configuration separate from images and inject environment-specific values at deployment time.

## Scaling and Reliability

- Horizontal scaling increases the number of pod replicas.
- Vertical scaling changes the resources assigned to a workload.
- Autoscaling adjusts capacity based on measured demand.
- Rolling updates replace old pods gradually.
- Readiness probes control whether a pod receives traffic.
- Liveness probes identify containers that need restarting.

## Operational Costs and Risks

Kubernetes provides powerful control but adds complexity in networking, security, upgrades, observability, and incident response. Use a managed service such as [[Azure Cloud|Azure Kubernetes Service]] when appropriate, but retain responsibility for workload configuration and cluster practices.

## Useful Commands

```powershell
kubectl get pods
kubectl get deployments
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl apply -f deployment.yaml
kubectl rollout status deployment/web-api
```

## Related Concepts

- [[Docker Basics]] - Build and run container images
- [[Azure Cloud]] - Managed Kubernetes and cloud infrastructure
- [[DevOps]] - Operate and improve deployed systems
- [[CI-CD Pipeline]] - Automate manifest and image delivery
