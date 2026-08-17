---
tags:
  - csharp
  - oop
category: C# Language
related: Interfaces, Inheritance, Access Modifiers
---

# Classes

A class is a blueprint or template for creating objects. It defines the structure and behavior that instances of the class will have.

## Core Concepts

Classes are the foundation of object-oriented programming in C#. They encapsulate data (fields/properties) and behavior (methods) into a single reusable unit.

### Members

A class can contain:
- **Fields** - Variables that store data for the object
- **Properties** - Controlled access to fields via getters/setters
- **Methods** - Functions that define object behavior
- **Constructors** - Special methods that initialize new objects
- **Events** - Mechanisms for object communication

## Basic Syntax

```csharp
public class Person
{
    // Field
    private string name;
    
    // Property
    public string Name { get; set; }
    
    // Constructor
    public Person(string name)
    {
        Name = name;
    }
    
    // Method
    public void Greet()
    {
        Console.WriteLine($"Hello, I'm {Name}");
    }
}
```

## Key Principles

- **Encapsulation** - Hide internal implementation, expose only what's necessary
- **Inheritance** - [[Classes]] can inherit from base classes to reuse code
- **Polymorphism** - Derived classes can override methods for different behavior
- **Access Modifiers** - Control visibility: `public`, `private`, `protected`, `internal`

## Related Concepts

- [[Inheritance]] - How classes extend other classes
- [[Interfaces]] - How to define contracts for classes
- [[Access Modifiers]] - Controlling class member visibility
- [[Namespaces]] - Organizing classes logically
- [[OOP Fundamentals]] - Theoretical foundation