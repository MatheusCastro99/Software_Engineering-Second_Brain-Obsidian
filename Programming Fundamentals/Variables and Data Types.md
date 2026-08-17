---
tags:
  - fundamentals
  - csharp
category: Programming Fundamentals
related: Operators, Methods, Error Handling
---

# Variables and Data Types

Variables are containers that store data in memory. C# is **strongly typed**, meaning every variable must have a declared type that determines what kind of data it can hold.

## Key Characteristics

- **Strongly Typed** - Type must be specified at declaration; type checking happens at compile time
- **Memory Allocation** - Variables reserve space in memory when declared
- **Initialization** - Variables should be initialized before use to avoid null reference errors
- **Scope** - Variables exist within their declared scope (method, class, namespace)

## Built-in Data Types

### Value Types (Stack)
- **int** - 32-bit integer (-2.1B to 2.1B)
- **long** - 64-bit integer (larger range)
- **double** - 64-bit floating point (15-17 digits precision)
- **float** - 32-bit floating point (7 digits precision)
- **bool** - Boolean (true/false)
- **char** - Single Unicode character
- **decimal** - 128-bit for financial calculations (28-29 significant digits)

### Reference Types (Heap)
- **string** - Immutable sequence of characters
- **object** - Base type for all C# types
- **DateTime** - Date and time values
- **Arrays** - Collections of same-type elements

## Variable Declaration Patterns

```csharp
// Explicit type
int age = 25;
string name = "Alice";

// Implicit type (var keyword)
var salary = 50000.00; // inferred as double

// Constants (immutable)
const double PI = 3.14159;
readonly string AppName = "MyApp";

// Nullable types
int? nullableInt = null;
string? optionalString = null;
```

## Const vs Readonly

| Feature | const | readonly |
|---------|-------|----------|
| **Initialized** | At declaration only | At declaration or constructor |
| **Static** | Always static | Can be instance or static |
| **Scope** | Compile-time | Runtime |
| **Use Case** | Never-changing literals | Values set once per object |

## Type Conversion

Converting between types requires explicit casting to avoid data loss:

```csharp
// Implicit (safe)
double myDouble = 100; // int → double automatically

// Explicit (casting)
int myInt = (int)myDouble; // double → int (may lose precision)

// Conversion methods
string text = "42";
int number = int.Parse(text);
bool success = int.TryParse(text, out int result);
```

## Related Concepts

- [[Operators]] - Perform operations on variables
- [[Methods]] - Functions to work with data
- [[Memory Management]] - How variables are stored in memory
- [[Error Handling]] - Managing null and type errors