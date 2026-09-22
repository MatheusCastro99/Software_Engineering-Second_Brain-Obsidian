---
tags:
  - architecture
  - clean-architecture
  - design
category: Architecture Conventions and Templates
related: SOLID Principles, Interfaces, Feature-oriented, Monolith - Modular Monolith
---

# Clean Code Architecture (Clean Architecture)

Clean Architecture, described by Robert C. Martin ("Uncle Bob"), organizes an application into concentric layers with the business rules at the center and technical details (UI, database, frameworks) on the outside. Its single most important rule is the **Dependency Rule**: source code dependencies always point **inward**. The core never knows which database, web framework, or UI is being used.

## The Layers

```text
┌──────────────────────────────────────────────┐
│  Infrastructure / Frameworks & Drivers       │  EF Core, SQL, file system, external APIs
│  ┌────────────────────────────────────────┐  │
│  │  Interface Adapters / Presentation     │  │  Controllers, ViewModels, repositories
│  │  ┌──────────────────────────────────┐  │  │
│  │  │  Application (Use Cases)         │  │  │  PlaceOrder, RegisterUser
│  │  │  ┌────────────────────────────┐  │  │  │
│  │  │  │  Domain (Entities)         │  │  │  │  Order, Customer, business rules
│  │  │  └────────────────────────────┘  │  │  │
│  │  └──────────────────────────────────┘  │  │
│  └────────────────────────────────────────┘  │
└──────────────────────────────────────────────┘
           Dependencies point inward ──►
```

| Layer | Contains | Depends on |
|-------|----------|------------|
| **Domain** | Entities, value objects, core rules | Nothing |
| **Application** | Use cases, interfaces the app needs (`IOrderRepository`) | Domain |
| **Infrastructure** | Database, email, file, API implementations | Application, Domain |
| **Presentation** | Controllers, ViewModels, UI | Application |

## Dependency Inversion in Practice

The inner layer defines an interface. The outer layer implements it. Dependency injection connects them at startup.

```csharp
// Application layer: defines what it needs
public interface IOrderRepository
{
    Order? GetById(int id);
    void Save(Order order);
}

public class PlaceOrderHandler
{
    private readonly IOrderRepository _orders;

    public PlaceOrderHandler(IOrderRepository orders) => _orders = orders;

    public void Handle(Order order)
    {
        order.Validate();          // Domain rule
        _orders.Save(order);       // Doesn't know it's SQL
    }
}

// Infrastructure layer: implements it
public class SqlOrderRepository : IOrderRepository
{
    public Order? GetById(int id) { /* EF Core query */ return null; }
    public void Save(Order order) { /* EF Core insert */ }
}

// Program.cs (composition root)
builder.Services.AddScoped<IOrderRepository, SqlOrderRepository>();
```

Swapping SQL Server for another database only changes the Infrastructure project.

## Typical .NET Solution Layout

```text
MyApp.sln
├── MyApp.Domain/           # entities, no package references
├── MyApp.Application/      # use cases + interfaces, references Domain
├── MyApp.Infrastructure/   # EF Core, email, references Application
└── MyApp.Api/              # controllers, DI setup, references Application + Infrastructure
```

Project references enforce the Dependency Rule at compile time: Domain cannot accidentally reference EF Core.

## Clean Code Practices That Support It

The architecture works best when the code inside each layer is clean as well:
- **Meaningful names** - `CalculateInvoiceTotal()` instead of `Calc()`
- **Small, focused methods** - one level of abstraction per method
- **Single responsibility** - see [[SOLID Principles]]
- **No duplication** - see [[DRY Principle]]
- **Explicit error handling** - see [[Error Handling]]
- **Tests** - use cases can be tested with fake repositories and no database

## Advantages and Trade-offs

**Advantages**
- Business rules are independent of frameworks, UI, and database
- Highly testable core
- Infrastructure can be replaced or upgraded with limited impact

**Trade-offs**
- More projects, interfaces, and mapping code
- Can feel heavy for simple CRUD apps
- Needs team discipline to keep dependencies pointing inward

## Use when

- The domain has real business rules worth protecting
- The app is expected to live and change for years
- Multiple front ends (API, UI, background jobs) share the same logic

## Related Concepts

- [[SOLID Principles]] - Dependency inversion is the core mechanism
- [[Interfaces]] - Contracts defined by inner layers
- [[Feature-oriented]] - Alternative or complement: slice by feature instead of layer
- [[Monolith - Modular Monolith]] - Clean Architecture is often applied inside each module
- [[MVC]] - Controllers live in the presentation layer
- [[Technical Debt]] - Clear boundaries reduce design debt
