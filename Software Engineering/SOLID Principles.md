---
tags:
  - software-engineering
  - design
  - principles
category: Software Engineering
related: OOP Fundamentals, Classes, Interfaces, DRY Principle
---

# SOLID Principles

SOLID is an acronym for five design principles that help create maintainable, scalable, and robust code. These principles guide object-oriented design.

## S - Single Responsibility Principle (SRP)

**A class should have only one reason to change.**

- Each class should have a single, well-defined responsibility
- Reduces coupling and increases maintainability

```csharp
// Bad: Multiple responsibilities
public class User
{
    public void Save() { } // Persistence
    public string Validate() { } // Validation
    public void SendEmail() { } // Communication
}

// Good: Single responsibility
public class User { }
public class UserRepository { public void Save(User u) { } }
public class UserValidator { public string Validate(User u) { } }
public class EmailService { public void Send(User u) { } }
```

## O - Open/Closed Principle (OCP)

**Software entities should be open for extension, closed for modification.**

- Extend behavior without modifying existing code
- Use [[Interfaces]] and [[Inheritance]] for extension
- Reduces risk of breaking existing functionality

```csharp
// Bad: Must modify for each new discount type
public class PriceCalculator
{
    public decimal Calculate(string type)
    {
        if (type == "Student") return price * 0.9m;
        if (type == "Senior") return price * 0.8m;
    }
}

// Good: Extend via interface
public interface IDiscountStrategy { decimal Apply(decimal price); }
public class StudentDiscount : IDiscountStrategy { }
public class SeniorDiscount : IDiscountStrategy { }
```

## L - Liskov Substitution Principle (LSP)

**Objects of a superclass should be replaceable with objects of its subclasses without breaking the application.**

- Derived classes must be substitutable for base classes
- Violating this breaks polymorphism
- Ensures proper [[Inheritance]] design

```csharp
// Bad: Bird can't fly
public class Bird { public virtual void Fly() { } }
public class Penguin : Bird { public override void Fly() { throw new Exception(); } }

// Good: Separate concerns
public interface IFlying { void Fly(); }
public class Sparrow : IFlying { }
public class Penguin { } // Not flying
```

## I - Interface Segregation Principle (ISP)

**Clients should not be forced to depend on interfaces they don't use.**

- Create specific, focused [[Interfaces]]
- Better than one large interface with unused methods
- Improves flexibility and testability

```csharp
// Bad: Force all methods on all workers
public interface IWorker { void Work(); void Eat(); }
public class Robot : IWorker { public void Eat() { throw new NotImplemented(); } }

// Good: Segregate into specific interfaces
public interface IWorkable { void Work(); }
public interface IEatable { void Eat(); }
public class Robot : IWorkable { }
public class Human : IWorkable, IEatable { }
```

## D - Dependency Inversion Principle (DIP)

**High-level modules should not depend on low-level modules. Both should depend on abstractions.**

- Depend on interfaces, not concrete classes
- Enables loose coupling and testability
- Makes code more flexible and maintainable

```csharp
// Bad: Direct dependency on concrete class
public class PaymentService
{
    private SqlRepository repo = new SqlRepository();
}

// Good: Depend on abstraction
public class PaymentService
{
    private readonly IRepository repo;
    public PaymentService(IRepository repo) { this.repo = repo; }
}
```

## Summary Benefits

| Principle | Benefit |
|-----------|--------|
| **SRP** | Easy to understand and modify |
| **OCP** | Easy to extend without risk |
| **LSP** | Polymorphism works reliably |
| **ISP** | Cleaner interfaces, less coupling |
| **DIP** | Flexible, testable, maintainable |

## Related Concepts

- [[OOP Fundamentals]] - Foundation for these principles
- [[Classes]] - Where principles are applied
- [[Interfaces]] - Key tool for most principles
- [[DRY Principle]] - Complementary design principle