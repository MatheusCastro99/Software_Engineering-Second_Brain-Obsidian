---
tags:
  - architecture
  - design-patterns
  - web-development
category: Architecture Conventions and Templates
related: MVVM, Client-Server Architecture, REST API, SOLID Principles
---

# MVC (Model - View - Controller)

MVC is an architectural pattern that splits an application into three roles: the **Model** holds data and business rules, the **View** presents data to the user, and the **Controller** receives input, coordinates the work, and chooses what to return. The goal is separation of concerns: presentation can change without rewriting business logic, and logic can be tested without a UI.

## The Three Roles

| Role | Responsibility | Should NOT |
|------|----------------|------------|
| **Model** | Data, validation, business rules, state | Know how it is displayed |
| **View** | Render data (HTML, UI) | Contain business logic or data access |
| **Controller** | Handle requests, call the model, pick a view/response | Hold business rules itself ("fat controller") |

## Request Flow

```text
User action / HTTP request
        │
        ▼
   Controller ──► Model (read/update data, apply rules)
        │
        ▼
      View (rendered with model data)
        │
        ▼
    Response to user
```

In web MVC, a router maps the URL to a controller action. The action works with the model and returns a view or data.

## Example (ASP.NET Core MVC)

```csharp
// Model
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; } = "";
    public decimal Price { get; set; }
}

// Controller
public class ProductsController : Controller
{
    private readonly IProductService _service;

    public ProductsController(IProductService service) => _service = service;

    // GET /products
    public IActionResult Index()
    {
        List<Product> products = _service.GetAll();
        return View(products); // passes the model to Views/Products/Index.cshtml
    }
}
```

```html
<!-- View: Views/Products/Index.cshtml (Razor) -->
@model List<Product>
<ul>
@foreach (var p in Model)
{
    <li>@p.Name - @p.Price.ToString("C")</li>
}
</ul>
```

For APIs, the same controller structure returns JSON instead of a view, so the "View" becomes the serialized response (see [[Serializations]] and [[REST API]]).

## Common Mistakes

- **Fat controllers** - business rules written directly in actions. Move them into services or the model.
- **Logic in views** - calculations or data access inside templates.
- **Anemic models everywhere** - models become plain data bags while logic scatters across controllers.

## Advantages and Trade-offs

**Advantages**
- Clear separation of presentation, input handling, and logic
- Controllers and models are unit-testable
- Several views can reuse the same model
- Well supported by frameworks (ASP.NET Core, Spring, Rails, Django-style MTV)

**Trade-offs**
- More files and indirection for very small apps
- Controllers tend to grow without discipline
- Less suited to rich, stateful desktop UIs, where [[MVVM]] data binding fits better

## Use when

- Building server-rendered web applications or web APIs
- A request/response model fits the app
- The framework already follows MVC conventions (ASP.NET Core)

## Related Concepts

- [[MVVM]] - Binding-based alternative for desktop and mobile UIs
- [[Client-Server Architecture]] - MVC usually runs on the server side of this model
- [[REST API]] - API controllers expose resources over HTTP
- [[Clean Code]] - Keeping controllers thin and logic in inner layers
- [[SOLID Principles]] - Single responsibility for each role
- [[Popular Stacks and Frameworks]] - Frameworks that implement MVC
