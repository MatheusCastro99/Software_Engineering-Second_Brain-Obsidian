---
tags:
  - software-engineering
  - oop
  - design
category: Software Engineering
related: Classes, Interfaces, SOLID Principles, DRY Principle
---

# OOP Fundamentals

Object-Oriented Programming (OOP) is a programming paradigm that organizes code around "objects" that combine data and behavior. It's built on four core pillars.

## The Four Pillars

### 1. Encapsulation
**Bundling data and methods together; hiding internal details**

- Combine related data and functions into objects
- Use [[Access Modifiers]] to control what's exposed
- Hide complexity; expose simple interfaces
- Example: A `BankAccount` class hides transaction details, exposes `Deposit()` and `Withdraw()`

### 2. Abstraction
**Simplifying complexity by modeling real-world concepts**

- Focus on *what* an object does, not *how* it does it
- Hide implementation details behind clear interfaces
- Use [[Interfaces]] to define contracts
- Example: A `Vehicle` class abstracts common behavior without exposing engine mechanics

### 3. Inheritance
**Creating hierarchies to reuse and extend code**

- Child classes inherit properties and methods from parent classes
- Enables code reuse and establishes relationships
- Use [[Classes]] to model "is-a" relationships
- Example: `Dog` and `Cat` inherit from `Animal`

### 4. Polymorphism
**Objects of different types responding to the same message differently**

- Same method name, different implementations per class
- Achieved through method overriding and [[Interfaces]]
- Enables flexible, extensible code
- Example: `Animal.MakeSound()` produces different results for `Dog` vs `Cat`

## Benefits of OOP

✓ **Modularity** - Code organized into logical, reusable units
✓ **Maintainability** - Easier to understand and modify
✓ **Reusability** - Classes can be reused across projects
✓ **Flexibility** - Polymorphism allows runtime behavior changes
✓ **Scalability** - Scales well with large codebases

## OOP vs Procedural Programming

| OOP | Procedural |
|-----|------------|
| Data and functions bundled in objects | Data separate from functions |
| Models real-world entities | Sequence of operations |
| Easier to maintain large systems | Simpler for small scripts |
| Inheritance and polymorphism | Limited code reuse |

## Real-World Example

```csharp
// Abstraction + Encapsulation
public abstract class Animal
{
    protected string Name; // Encapsulation
    
    public abstract void MakeSound(); // Abstraction
}

// Inheritance
public class Dog : Animal
{
    public override void MakeSound() // Polymorphism
    {
        Console.WriteLine("Woof!");
    }
}

public class Cat : Animal
{
    public override void MakeSound() // Polymorphism
    {
        Console.WriteLine("Meow!");
    }
}
```

## Related Concepts

- [[Classes]] - Building blocks of OOP
- [[Interfaces]] - Defining contracts
- [[SOLID Principles]] - Design principles for OOP
- [[DRY Principle]] - Avoid code duplication