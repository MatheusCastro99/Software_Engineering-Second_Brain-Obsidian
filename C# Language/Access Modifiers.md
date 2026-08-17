---
tags:
  - csharp
  - encapsulation
category: C# Language
related: Classes, Interfaces, Inheritance, OOP Fundamentals
---

# Access Modifiers

Access modifiers control the visibility and accessibility of class members (fields, properties, methods) from different parts of your code. They're essential for [[Encapsulation]].

## Visibility Levels

### public
- **Accessible from** - Anywhere (any class, namespace)
- **Use case** - Public API, intended for external use
- **Least protective** - Exposes implementation details

```csharp
public string Name { get; set; }
```

### private
- **Accessible from** - Only within the same class
- **Use case** - Internal implementation, helper methods
- **Most protective** - Default if no modifier specified
- **Best for** - Hiding complexity

```csharp
private decimal CalculateTax() { }
```

### protected
- **Accessible from** - Same class and derived (child) classes
- **Use case** - Implementation meant for subclasses
- **Enables** - Controlled [[Inheritance]]

```csharp
protected virtual void OnDataChanged() { }
```

### internal
- **Accessible from** - Same assembly (project) only
- **Use case** - Internal framework, cross-class sharing
- **Scope** - Assembly-level encapsulation

```csharp
internal class HelperClass { }
```

### protected internal
- **Accessible from** - Same assembly OR derived classes (OR both)
- **Use case** - Rare; useful for framework code

## Comparison Table

| Modifier | Same Class | Derived Class | Same Assembly | Outside Assembly |
|----------|-----------|---------------|--------------|------------------|
| **public** | ✓ | ✓ | ✓ | ✓ |
| **protected** | ✓ | ✓ | ✗ | ✗ |
| **internal** | ✓ | ✗ | ✓ | ✗ |
| **protected internal** | ✓ | ✓ | ✓ | ✗ |
| **private** | ✓ | ✗ | ✗ | ✗ |

## Best Practices

✓ **Default to private** - Only expose what's necessary
✓ **Use properties** - Hide fields, expose through `{ get; set; }`
✓ **Minimal public API** - Reduces coupling
✓ **Progressive exposure** - Start private, make public only when needed

## Example: Proper Encapsulation

```csharp
public class BankAccount
{
    private decimal balance; // Private field
    
    public decimal Balance { get; private set; } // Read-only property
    
    public void Deposit(decimal amount)
    {
        if (amount > 0) balance += amount;
    }
    
    private void ValidateAccount() // Private helper
    {
        // Internal logic only
    }
}
```

## Related Concepts

- [[Classes]] - Where modifiers are applied
- [[OOP Fundamentals]] - Encapsulation pillar
- [[Inheritance]] - Protected enables inheritance design

- Public
- Internal
- Protected
- Private

Used for encapsulation.