---
tags:
  - csharp
  - oop
  - design
category: C# Language
related: Classes, Inheritance, Access Modifiers, SOLID Principles
---

# Interfaces

An interface is a contract that defines a set of methods and properties that a class must implement. It specifies *what* a class should do, not *how* to do it.

## Core Concepts

### Syntax

```csharp
public interface IShape
{
    void Draw();
    double Area { get; }
}

public class Circle : IShape
{
    public void Draw() => Console.WriteLine("Drawing circle");
    public double Area => Math.PI * radius * radius;
}
```

### Key Characteristics

- **No implementation** - Only method signatures (not enforcing in modern C#)
- **Multiple implementation** - A class can implement multiple interfaces
- **Contracts** - Define a "promise" of functionality
- **Polymorphism** - Different classes satisfy same interface differently

## Interface vs Abstract Class

| Aspect | Interface | Abstract Class |
|--------|-----------|----------------|
| **Members** | Methods/Properties | Methods/Fields/Properties |
| **Inheritance** | Multiple | Single |
| **State** | None | Can have state |
| **Purpose** | Contract | Base implementation |
| **Use Case** | "What it can do" | "What it is" |

## Benefits

✓ **Loose Coupling** - Depend on abstractions, not concrete classes
✓ **Flexible Design** - Easy to swap implementations
✓ **Multiple Implementation** - Achieve multiple inheritance of type
✓ **Testability** - Easy to create mock implementations
✓ **Follows SOLID** - Especially Interface Segregation Principle

## Real-World Example

```csharp
public interface IRepository
{
    T GetById(int id);
    void Save(T entity);
}

public class SqlRepository : IRepository { }
public class MongoRepository : IRepository { }

// Can swap implementations without changing business logic
public class UserService
{
    private readonly IRepository repo;
    
    public UserService(IRepository repo) // Dependency injection
    {
        this.repo = repo;
    }
}
```

## Related Concepts

- [[Classes]] - Implement interfaces
- [[Inheritance]] - Interfaces enable polymorphic inheritance
- [[Access Modifiers]] - Interface member visibility
- [[SOLID Principles]] - Interface Segregation Principle

Interfaces define contracts.

Benefits:
- Loose coupling
- Composition
- Dependency inversion