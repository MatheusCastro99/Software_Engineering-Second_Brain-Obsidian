---
tags:
	- shipping-solutions
	- docker
	- containers
category: Shipping Solutions
related: Docker commands, Kubernetes, Azure Cloud, ForEach-Object $_ and other useful tricks
---

# Docker Basics

Docker packages an application and its runtime requirements into a portable container image. A container is an isolated process running on a host operating system. Containers are not small virtual machines: virtual machines emulate hardware and run a guest operating system, while containers share the host kernel.

## Images and Containers

- **Image** - Read-only, layered template containing application code, dependencies, and filesystem content.
- **Container** - A running instance of an image with a writable runtime layer, process, network, and resource settings.
- **Registry** - Repository that stores and distributes images, such as Docker Hub or a private registry.
- **Dockerfile** - Text instructions used to build an image.

```text
Dockerfile -> docker build -> Image -> docker run -> Container
```

An image should contain the requirements for the application to run, but not secrets or environment-specific configuration. Supply those at runtime.

## Containers vs. Virtual Machines

| Concern | Virtual machine | Container |
|---------|-----------------|-----------|
| Isolation boundary | Virtual hardware and guest OS | Process and kernel features |
| Startup | Usually slower | Usually faster |
| Image size | Includes a full operating system | Shares host kernel and layers |
| Compatibility | Can run a different guest OS | Must be compatible with the host kernel model |
| Typical use | Strong OS isolation and legacy systems | Portable services and repeatable environments |

## Linux Namespaces and Control Groups

Container isolation is provided by operating-system features rather than a complete guest OS.

Common Linux namespaces include:

| Namespace | Isolates the container's view of |
|-----------|----------------------------------|
| Mount | Filesystem mount points |
| PID | Processes and process IDs |
| Network | Interfaces, routes, and ports |
| IPC | Inter-process communication resources |
| UTS | Hostname and domain name |
| User | User and group IDs |
| Cgroup | Control-group hierarchy visibility |
| Time | System clocks and offsets |

Control groups, or cgroups, limit and account for resources such as CPU, memory, and processes. Namespaces isolate what a process can see; cgroups limit what it can consume. Neither should be treated as an absolute security boundary without additional hardening.

## Dockerfile Example

```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
EXPOSE 8080

COPY . .
ENTRYPOINT ["dotnet", "Example.Api.dll"]
```

Production Dockerfiles often use multi-stage builds so the final image contains the runtime and published application, but not the SDK or build artifacts.

## Storage and Networking

Container filesystems are temporary by default. Use volumes for data that must survive container replacement. Container networks allow services to communicate without exposing every internal port to the host.

```powershell
docker volume create app-data
docker network create app-network
```

## Docker Desktop

Docker Desktop provides a graphical interface and a local Docker engine for Windows and macOS. It can manage images, containers, volumes, networks, logs, and resource settings. The GUI complements the command line; commands and configuration are easier to automate and reproduce in scripts and CI/CD pipelines.

## Best Practices

- Use small, pinned base images and update them regularly.
- Run as a non-root user when practical.
- Add a `.dockerignore` file to reduce build context.
- Never bake secrets into images.
- Tag images with an immutable version or commit identifier.
- Scan images and remove unnecessary packages.
- Define CPU and memory limits for shared environments.
- Log to standard output and let the platform collect logs.

## Related Concepts

- [[Docker commands]] - Build, run, inspect, and manage containers
- [[Kubernetes]] - Orchestrate containers at scale
- [[Azure Cloud]] - Host and manage container workloads
- [[CI-CD Pipeline]] - Build and publish images automatically
- [[ForEach-Object $_ and other useful tricks]] - Automate Docker tasks with PowerShell