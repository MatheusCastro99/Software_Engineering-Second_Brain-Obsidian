---
tags:
  - architecture
  - monolith
  - system-design
category: Architecture Conventions and Templates
related: Microservices Architecture, Feature-oriented, Clean Code, Docker Basics
---

# Monolith and Modular Monolith

A **monolith** is an application built and deployed as a **single unit**: one codebase, one build, one process, and usually one database. A **modular monolith** keeps that single deployment but divides the inside into **independent modules** with clear boundaries. Each module owns its own code and data and talks to other modules only through public contracts.

## Traditional Monolith

```text
┌─────────────────────────────────────┐
│           MyApp (one deploy)        │
│  Controllers ─ Services ─ Repos     │
│  Orders, Users, Payments all mixed  │
└──────────────────┬──────────────────┘
                   │
            ┌──────▼──────┐
            │  One DB     │
            └─────────────┘
```

**Strengths**
- Simple to build, run, debug, and deploy
- Function calls instead of network calls: fast and reliable
- Transactions across the whole app are easy

**Problems as it grows ("big ball of mud")**
- Everything can reference everything, which creates tight coupling
- A small change requires redeploying the whole app
- Hard for several teams to work in parallel
- The whole app scales as one unit

## Modular Monolith

```text
┌──────────────────────────────────────────────┐
│              MyApp (one deploy)              │
│  ┌──────────┐   ┌──────────┐   ┌──────────┐  │
│  │  Orders  │   │  Users   │   │ Payments │  │
│  │  module  │◄─►│  module  │◄─►│  module  │  │
│  └────┬─────┘   └────┬─────┘   └────┬─────┘  │
│       │ public contracts / events only       │
└───────┼──────────────┼──────────────┼────────┘
   orders schema   users schema   payments schema
```

Rules that make it modular:
- Each module has a **public API** (interfaces, DTOs, events). Internals stay `internal`.
- Modules do not read each other's tables. Each owns its own schema or tables.
- Cross-module calls go through the public API or in-process events.
- Boundaries follow **business capabilities**, like in [[Feature-oriented]] design.

## Example: Enforcing Boundaries in C#

```csharp
// Orders.Contracts project: the only thing other modules may reference
public interface IOrdersModule
{
    Task<OrderSummary?> GetOrderAsync(int orderId);
}
public record OrderSummary(int Id, decimal Total);

// Orders module project: implementation stays internal
internal class OrdersModule : IOrdersModule
{
    private readonly OrdersDbContext _db;
    public OrdersModule(OrdersDbContext db) => _db = db;

    public async Task<OrderSummary?> GetOrderAsync(int orderId)
    {
        var order = await _db.Orders.FindAsync(orderId);
        return order is null ? null : new OrderSummary(order.Id, order.Total);
    }
}
```

[[Access Modifiers]] (`internal`) and separate projects make the boundary a compile-time rule, not just a convention.

## Monolith vs Modular Monolith vs Microservices

| Aspect | Monolith | Modular Monolith | [[Microservices Architecture\|Microservices]] |
|--------|----------|------------------|---------------|
| Deployment | One unit | One unit | Many independent units |
| Internal boundaries | Weak or none | Strong, enforced | Network boundaries |
| Communication | Direct calls | Contracts / in-process events | HTTP, gRPC, messaging |
| Data | Shared DB | Schema per module | DB per service |
| Operational complexity | Low | Low | High |
| Independent scaling | No | No | Yes |

A modular monolith is often the recommended **starting point**: it gives most of the organizational benefits of microservices without distributed-system complexity. A well-bounded module can later be extracted into a service if it truly needs independent scaling or deployment.

## Use when

- **Monolith** - small apps, prototypes, small teams, simple domains
- **Modular monolith** - growing apps with several business areas, when one deployment is still acceptable

## Related Concepts

- [[Microservices Architecture]] - The distributed alternative
- [[Feature-oriented]] - Organizing code by business feature, the basis for modules
- [[Clean Code]] - Layering applied inside each module
- [[Access Modifiers]] - `internal` keeps module internals hidden
- [[Docker Basics]] - Packaging the single deployable unit
- [[Technical Debt]] - Unbounded monoliths accumulate design debt
