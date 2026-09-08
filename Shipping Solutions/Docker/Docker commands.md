---
tags:
	- shipping-solutions
	- docker
	- command-line
category: Shipping Solutions
related: Docker Basics, Kubernetes, ForEach-Object $_ and other useful tricks
---

# Docker Commands

Docker commands manage images, containers, networks, volumes, and registries. The usual workflow is to build or pull an image, run a container, inspect its behavior, and remove or redeploy it when the application changes.

## Images

```powershell
docker pull nginx:latest
docker images
docker build -t example-api:1.0.0 .
docker tag example-api:1.0.0 registry.example.com/example-api:1.0.0
docker push registry.example.com/example-api:1.0.0
docker rmi example-api:1.0.0
```

Prefer explicit version tags for deployments. `latest` is convenient for experiments but is mutable and difficult to audit.

## Containers

```powershell
docker run --name example-api -d -p 8080:8080 example-api:1.0.0
docker ps
docker ps -a
docker logs --follow example-api
docker exec -it example-api sh
docker inspect example-api
docker stop example-api
docker start example-api
docker rm example-api
```

`-d` runs in detached mode, `-p` maps host and container ports, and `--name` makes later commands easier to read.

## Environment and Volumes

```powershell
docker run --rm `
	--env ASPNETCORE_ENVIRONMENT=Development `
	--mount type=volume,source=app-data,target=/app/data `
	--name example-api example-api:1.0.0
```

Use `--rm` for temporary containers. Use named volumes or bind mounts when files must survive container replacement. Keep secrets out of command history when possible by using a secure secret mechanism.

## Networks

```powershell
docker network create app-network
docker run -d --network app-network --name database postgres:16
docker network ls
docker network inspect app-network
docker network rm app-network
```

Containers on the same user-defined network can resolve one another by container name. Expose only the ports that must be reachable from the host or outside network.

## Cleanup

```powershell
docker container prune
docker image prune
docker volume prune
docker system df
docker system prune
```

Prune commands delete unused resources. Review what will be removed before using them on a machine that contains important development data.

## Compose Workflows

Docker Compose describes a multi-container application in a YAML file:

```powershell
docker compose up --build -d
docker compose ps
docker compose logs --follow
docker compose down
```

Use Compose for local development and repeatable integration environments. Persistent volumes and environment files should be handled deliberately.

## Troubleshooting Sequence

1. Check whether the container is running with `docker ps -a`.
2. Read application output with `docker logs <name>`.
3. Inspect ports, environment, mounts, and status with `docker inspect <name>`.
4. Test connectivity from the correct network.
5. Confirm the image tag and configuration match the intended version.
6. Rebuild without stale layers only when the evidence suggests a cache issue.

## Related Concepts

- [[Docker Basics]] - Images, containers, isolation, and storage
- [[Kubernetes]] - Use declarative orchestration for many containers
- [[ForEach-Object $_ and other useful tricks]] - PowerShell automation
- [[CI-CD Pipeline]] - Automate image builds and publishing
