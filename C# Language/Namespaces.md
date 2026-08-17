---
tags:
  - csharp
  - organization
category: C# Language
related: Classes, Access Modifiers
---

# Namespaces

A namespace is a container that organizes code into logical groups and prevents naming conflicts. It's the C# way of creating hierarchy in large projects.

## Purpose

- **Organization** - Group related classes logically
- **Avoid Conflicts** - Two classes can have same name in different namespaces
- **Encapsulation** - Organize code at project level
- **Convention** - Follow organizational structure: `Company.Project.Feature`

## Syntax

```csharp
namespace MyApp.Core.Models
{
    public class User
    {
        public string Name { get; set; }
    }
}

namespace MyApp.Services
{
    public class UserService
    {
        // Must use 'using' or full path
        private User user; // Won't work without 'using'
        private MyApp.Core.Models.User user; // Works with full path
    }
}
```

## Using Statements

```csharp
using MyApp.Core.Models; // Import namespace
using UserService = MyApp.Services.UserService; // Alias

public class Program
{
    static void Main()
    {
        var user = new User(); // Now available due to 'using'
    }
}
```

## File-Scoped Namespaces (C# 10+)

```csharp
namespace MyApp.Services;

public class UserService // Automatically in MyApp.Services
{
}
```

## Naming Conventions

```
CompanyName.ProjectName.FeatureName.ComponentType

Examples:
Microsoft.EntityFrameworkCore
Newtonsoft.Json
MyCompany.Banking.Accounts.Models
MyCompany.Banking.Accounts.Services
```

## Best Practices

✓ **Match folder structure** - Namespace mirrors folder hierarchy
✓ **Use descriptive names** - Clear organization
✓ **Avoid deep nesting** - Keep 3-4 levels maximum
✓ **Group related types** - Similar concepts in same namespace
✗ **Avoid global namespace** - Always use namespaces
✗ **Avoid conflicts** - Unique names within scope

## Related Concepts

- [[Classes]] - Organized within namespaces
- [[Access Modifiers]] - Control visibility across namespaces

Namespaces organize code and prevent naming collisions.