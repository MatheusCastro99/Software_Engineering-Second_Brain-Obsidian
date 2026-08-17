---
tags:
  - software-engineering
  - principles
  - maintenance
category: Software Engineering
related: SOLID Principles, OOP Fundamentals, Methods, Classes
---

# DRY Principle

**Don't Repeat Yourself** - Every piece of knowledge should exist in exactly one place. Avoid duplicating code, logic, and configuration.

## Core Concept

When the same code appears in multiple places:
- Maintenance becomes harder (fix in 5+ places)
- Bugs can slip through (miss one location)
- Consistency suffers (implementations diverge)
- Code bloats unnecessarily

## Why DRY Matters

### The Cost of Duplication

```csharp
// Bad: Validation logic repeated
public void RegisterUser(string email)
{
    if (string.IsNullOrEmpty(email) || !email.Contains("@"))
        throw new Exception("Invalid email");
}

public void UpdateUser(string email)
{
    if (string.IsNullOrEmpty(email) || !email.Contains("@"))
        throw new Exception("Invalid email");
}

// Good: Extract to method
private bool IsValidEmail(string email)
    => !string.IsNullOrEmpty(email) && email.Contains("@");

public void RegisterUser(string email)
{
    if (!IsValidEmail(email)) throw new Exception("Invalid email");
}
```

## Common DRY Violations

### 1. Duplicated Logic
```csharp
// Bad
var discountedPrice1 = price * 0.9m;
var discountedPrice2 = price * 0.9m;

// Good
decimal ApplyDiscount(decimal price) => price * 0.9m;
```

### 2. Copy-Paste Code
```csharp
// Bad: Similar classes
public class UserRepository { public List<User> GetAll() { } }
public class ProductRepository { public List<Product> GetAll() { } }

// Good: Generic base class
public class Repository<T>
{
    public List<T> GetAll() { }
}
```

### 3. Magic Numbers
```csharp
// Bad
if (user.Age >= 18) { }
if (employee.Age >= 18) { }
if (voter.Age >= 18) { }

// Good
private const int LegalAge = 18;
if (user.Age >= LegalAge) { }
```

## How to Apply DRY

| Problem | Solution |
|---------|----------|
| Duplicated methods | Extract to shared method |
| Repeated patterns | Use [[Classes]] or inheritance |
| Configuration duplication | Use constants, config files |
| Similar classes | Use generics, base classes |
| Repeated conditions | Extract to method |

## DRY vs Over-Abstraction

⚠️ **Don't over-apply DRY**
- "Rule of Three" - Extract after seeing pattern 3 times
- Avoid premature abstraction
- Simple duplication is sometimes better than complex abstraction

```csharp
// Acceptable: Simple, clear duplication
var result1 = list1.Where(x => x.IsActive).ToList();
var result2 = list2.Where(x => x.IsActive).ToList();

// Over-engineered:
var result1 = FilterActive(list1);
var result2 = FilterActive(list2);
private List<T> FilterActive<T>(List<T> list) where T : IActive
    => list.Where(x => x.IsActive).ToList();
```

## Benefits

✓ **Easier Maintenance** - Changes in one place fix everything
✓ **Fewer Bugs** - Fix once, bug fixed everywhere
✓ **Cleaner Code** - Less code overall
✓ **Better Readability** - Intentions clearer
✓ **Faster Development** - Reuse existing code

## Related Concepts

- [[SOLID Principles]] - SRP aligns with DRY
- [[Classes]] - Organization tool for DRY
- [[Methods]] - Extract duplicated logic here
- [[OOP Fundamentals]] - Inheritance enables DRY