---
tags:
  - architecture
  - microservices
  - system-design
category: Architecture Conventions and Templates
related: Monolith - Modular Monolith, Docker Basics, Kubernetes, REST API
---

# Microservices Architecture

Microservices architecture is a service-oriented approach where an application is built as a set of **small, independently deployable services**. Each service is organized around one business capability, owns its own data, and communicates with other services over the network. Each service can be developed, deployed, and scaled by its own team without redeploying the rest of the system.

## Structure

```text
                 ┌──────────────┐
  Clients ─────► │ API Gateway  │
                 └──────┬───────┘
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
  ┌──────────┐   ┌──────────┐   ┌──────────┐
  │ Orders   │   │ Catalog  │   │ Payments │
  │ service  │   │ service  │   │ service  │
  └────┬─────┘   └────┬─────┘   └────┬─────┘
       ▼              ▼              ▼
   Orders DB     Catalog DB     Payments DB
        └─── events via message broker ───┘
```

## Key Characteristics

- **Single business capability** per service (Orders, Catalog, Payments)
- **Database per service** - no service reads another service's tables
- **Independent deployment** - each has its own build, version, and [[CI-CD Pipeline]]
- **Decentralized** - teams choose the tech that fits, within agreed standards
- **Designed for failure** - any network call can fail or be slow

## Communication

| Style | How | Example tools | Use for |
|-------|-----|---------------|---------|
| **Synchronous** | Request/response | HTTP/[[REST API]], gRPC | Queries that need an immediate answer |
| **Asynchronous** | Publish/subscribe events | RabbitMQ, Azure Service Bus, Kafka | Notifying other services that something happened |

```csharp
// Orders service publishes an event instead of calling Payments directly
public record OrderPlaced(int OrderId, decimal Total);

public class PlaceOrderHandler
{
    private readonly IMessagePublisher _bus;
    public PlaceOrderHandler(IMessagePublisher bus) => _bus = bus;

    public async Task Handle(Order order)
    {
        // save order in the Orders DB...
        await _bus.PublishAsync(new OrderPlaced(order.Id, order.Total));
    }
}
// The Payments service subscribes to OrderPlaced and charges the customer.
```

Asynchronous events reduce coupling: Orders keeps working even if Payments is temporarily down.

## Supporting Infrastructure

- **API Gateway** - single entry point, routing, authentication, rate limiting
- **Containers** - each service is packaged with [[Docker Basics|Docker]]
- **Orchestration** - [[Kubernetes]] runs, scales, and heals containers
- **Service discovery and configuration** - locate services and manage settings
- **Observability** - centralized logs, metrics, and distributed tracing (OpenTelemetry)
- **Resilience patterns** - retries, timeouts, circuit breakers (e.g., Polly in .NET)

## Challenges

- **Distributed data** - no cross-service transactions. Use eventual consistency and patterns like Saga and Outbox.
- **Network failures and latency** - every call can fail.
- **Operational overhead** - many pipelines, deployments, and dashboards.
- **Debugging** - a single request can cross many services.
- **Wrong boundaries** - services that constantly call each other become a "distributed monolith".

## Advantages and Trade-offs

**Advantages**
- Independent deployment and scaling per service
- Fault isolation: one failing service doesn't have to take down everything
- Teams own services end to end
- Technology flexibility per service

**Trade-offs**
- Much higher operational and architectural complexity
- Requires mature [[DevOps]], automation, and monitoring
- Premature adoption slows small teams down

## Use when

- Several teams need to deploy independently
- Parts of the system have very different scaling needs
- Business boundaries are well understood (often after starting as a [[Monolith - Modular Monolith|modular monolith]])

## Related Concepts

- [[Monolith - Modular Monolith]] - Simpler alternative and common starting point
- [[Feature-oriented]] - Business-capability boundaries that become services
- [[Docker Basics]] - Package each service as a container
- [[Kubernetes]] - Orchestrate services at scale
- [[Azure Cloud]] - Managed hosting (AKS, Container Apps, Service Bus)
- [[REST API]] - Synchronous service-to-service contracts
- [[Client-Server Architecture]] - Each service acts as a server to its clients
