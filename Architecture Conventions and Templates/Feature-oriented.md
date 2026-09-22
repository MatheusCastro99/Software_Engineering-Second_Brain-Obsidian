---
tags:
  - architecture
  - project-structure
  - design
category: Architecture Conventions and Templates
related: Clean Code, Monolith - Modular Monolith, Namespaces, MVC
---

# Feature-oriented Architecture

Feature-oriented architecture organizes files according to **business features** (Orders, Customers, Payments) instead of **technical function** (Controllers, Services, Repositories). Everything needed for one feature lives together, so a change to "checkout" touches one folder instead of five. It is also known as **feature folders** or, when each request is its own slice, **Vertical Slice Architecture**.

## Layer-based vs Feature-based

```text
Layer-based (by function)          Feature-based (by business feature)
─────────────────────────          ───────────────────────────────────
Controllers/                       Features/
  OrdersController.cs                Orders/
  CustomersController.cs               OrdersController.cs
Services/                              OrderService.cs
  OrderService.cs                      OrderRepository.cs
  CustomerService.cs                   Order.cs
Repositories/                          CreateOrderRequest.cs
  OrderRepository.cs                 Customers/
  CustomerRepository.cs                CustomersController.cs
Models/                                CustomerService.cs
  Order.cs                             Customer.cs
  Customer.cs
```

| Aspect | Layer-based | Feature-based |
|--------|-------------|---------------|
| Groups code by | Technical role | Business capability |
| Adding a feature touches | Many folders | One folder |
| Coupling risk | Features mix inside each layer | Features stay isolated |
| Team ownership | Split by layer | One team can own a feature |
| Discoverability | Easy to find "all controllers" | Easy to find "everything about Orders" |

## Vertical Slices

In Vertical Slice Architecture, each **use case** is a slice that contains its request, handler, validation, and response. Slices share as little as possible.

```csharp
// Features/Orders/CreateOrder.cs
namespace MyApp.Features.Orders;

public record CreateOrderRequest(int CustomerId, List<int> ProductIds);
public record CreateOrderResponse(int OrderId);

public class CreateOrderHandler
{
    private readonly AppDbContext _db;

    public CreateOrderHandler(AppDbContext db) => _db = db;

    public async Task<CreateOrderResponse> Handle(CreateOrderRequest request)
    {
        var order = new Order(request.CustomerId, request.ProductIds);
        _db.Orders.Add(order);
        await _db.SaveChangesAsync();
        return new CreateOrderResponse(order.Id);
    }
}
```

The [[Namespaces]] mirror the feature folders (`MyApp.Features.Orders`), which keeps related types together in IntelliSense and code search.

## Guidelines

- Name folders after business language (`Checkout`, `Invoices`), not technical terms.
- Keep truly shared code (logging, database context, common value objects) in a small `Shared/` or `Common/` folder.
- Avoid features calling deep into each other's internals. Communicate through public methods, events, or a mediator.
- Duplicating a small amount of code between slices is acceptable when it keeps features independent. Extract only when duplication becomes real (see [[DRY Principle]]).

## Advantages and Trade-offs

**Advantages**
- High cohesion: related code is together
- Changes stay local, which lowers the risk of side effects
- Scales well with team size and feature count
- Natural stepping stone toward a [[Monolith - Modular Monolith|modular monolith]] or [[Microservices Architecture|microservices]]

**Trade-offs**
- Shared logic needs deliberate placement
- Can lead to inconsistent patterns between features without conventions
- Less familiar to developers used to layer folders

## Use when

- The app has many distinct business features
- Multiple developers or teams work on different areas at the same time
- You want boundaries that could later become modules or services

## Related Concepts

- [[Clean Code]] - Layer-based alternative; the two can be combined (layers inside each feature)
- [[Monolith - Modular Monolith]] - Features grouped into enforced modules
- [[Microservices Architecture]] - Features split into separately deployed services
- [[Namespaces]] - Mirror the feature folder structure
- [[MVC]] - Controllers can live inside feature folders
