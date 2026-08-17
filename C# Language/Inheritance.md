---
tags:
  - csharp
  - oop
category: C# Language
related: Classes, Interfaces, Access Modifiers, OOP Fundamentals
---

# Inheritance

Inheritance is a mechanism that allows a class to inherit properties and methods from another class, enabling code reuse and establishing hierarchical relationships.

## Core Concepts

### Base Class vs Derived Class
- **Base Class** (Parent) - The class being inherited from
- **Derived Class** (Child) - The class that inherits from the base
- Derived class automatically gets all public and protected members of the base

### Syntax

```csharp
public class Animal // Base class
{
    public string Name { get; set; }
    public virtual void Speak() => Console.WriteLine("Animal sound");
}

public class Dog : Animal // Inheritance syntax
{
    public override void Speak() => Console.WriteLine("Woof!");
}
```

## Types of Inheritance

**Single Inheritance** (C# only supports this)
- A class inherits from ONE base class
- Multiple inheritance handled through [[Interfaces]]

## Virtual and Override

- **virtual** - Base class marks a method as overridable
- **override** - Derived class replaces the base implementation
- Enables **polymorphism** - different classes respond differently to same method call

## Access Modifiers and Inheritance

Understand [[Access Modifiers]] when inheriting:
- **public** - Accessible everywhere (including derived classes)
- **protected** - Accessible only in derived classes
- **private** - NOT inherited; inaccessible to derived classes

## Benefits

✓ **Code Reuse** - Inherit common functionality
✓ **Hierarchy** - Model real-world "is-a" relationships
✓ **Polymorphism** - Same interface, different implementations
✓ **Maintainability** - Changes to base class propagate to derived classes

## Related Concepts

- [[Classes]] - The building blocks of inheritance
- [[Interfaces]] - Alternative way to achieve polymorphism
- [[Access Modifiers]] - Control what's inherited
- [[OOP Fundamentals]] - Encapsulation, abstraction, polymorphism

Child classes extend parent classes.

Keywords: abstract, sealed, virtual, override.