---
tags:
  - fundamentals
  - csharp
  - functions
category: Programming Fundamentals
related: Classes, Operators, Variables and Data Types
---

# Methods

A method is a reusable block of code that performs a specific task. Methods are the foundation of modular, maintainable code.

## Anatomy of a Method

```csharp
public    decimal  CalculateTotal  (decimal price, int quantity)
  ^^      ^^^^^^^^  ^^^^^^^^^^^^^^^  ^^^^^^^^^^^^^^^^^^^^^^^^^
 Access   Return    Method Name      Parameters
 Modifier  Type
{
    return price * quantity;  // Method Body
}
```

## Method Components

- **Access Modifier** - Visibility: `public`, `private`, etc.
- **Return Type** - Data type returned: `int`, `string`, `void`, etc.
- **Method Name** - Descriptive identifier (PascalCase)
- **Parameters** - Input values (comma-separated)
- **Body** - Implementation code

## Parameters vs Arguments

```csharp
// Definition: "price" and "quantity" are PARAMETERS
public void Purchase(decimal price, int quantity)
{
    // ...
}

// Call: 99.99 and 5 are ARGUMENTS
Purchase(99.99m, 5);
```

| Term | Definition | Example |
|------|-----------|----------|
| **Parameter** | Variable in method definition | `public void Greet(string name)` - `name` is parameter |
| **Argument** | Value passed when calling | `Greet("Alice")` - `"Alice"` is argument |

## Return Values

```csharp
// Void - No return value
public void PrintMessage(string msg)
{
    Console.WriteLine(msg);
}

// Returns single value
public decimal CalculateDiscount(decimal price)
{
    return price * 0.1m;
}

// Tuple return - Multiple values (C# 7+)
public (string, int) GetPersonInfo()
{
    return ("Alice", 30);
}
var (name, age) = GetPersonInfo();
```

## Method Overloading

**Same method name, different parameters** - Enables flexibility and readability.

```csharp
// All valid - same name, different signatures
public void Print(string text) => Console.WriteLine(text);
public void Print(int number) => Console.WriteLine(number);
public void Print(string text, int count)
{
    for (int i = 0; i < count; i++) Console.WriteLine(text);
}

// Compiler chooses based on arguments
Print("Hello");        // Calls first
Print(42);             // Calls second
Print("Echo", 3);      // Calls third
```

## Optional Parameters

**Parameters with default values** - Callers can omit them.

```csharp
public void ConfigureServer(string host, int port = 8080, string protocol = "HTTP")
{
    Console.WriteLine($"{protocol}://{host}:{port}");
}

ConfigureServer("localhost");                    // Uses defaults
ConfigureServer("localhost", 3000);              // Override port
ConfigureServer("localhost", 443, "HTTPS");      // Override both
```

**Rules for optional parameters:**
- Must come after required parameters
- Must have default value
- Value must be constant at compile time

## Named Arguments

```csharp
public void Book(string name, string date, string room = "A1")
{
    Console.WriteLine($"{name} booked {room} on {date}");
}

// Traditional positional
Book("Meeting", "2024-01-15", "B2");

// Named arguments (any order)
Book(date: "2024-01-15", name: "Meeting", room: "B2");
Book(name: "Meeting", room: "B2", date: "2024-01-15");
```

## Output Parameters (out)

**Methods return multiple values via output parameters.**

```csharp
public bool TryParseInt(string text, out int result)
{
    if (int.TryParse(text, out result)) return true;
    result = 0;
    return false;
}

if (TryParseInt("42", out int number))
    Console.WriteLine($"Parsed: {number}");
```

## Reference Parameters (ref)

**Modify original variable passed by reference.**

```csharp
public void Increment(ref int value)
{
    value++; // Modifies original
}

int x = 5;
Increment(ref x);
Console.WriteLine(x); // 6
```

## Params Array

**Accept variable number of arguments.**

```csharp
public int Sum(params int[] numbers)
{
    int total = 0;
    foreach (int n in numbers) total += n;
    return total;
}

Sum(1, 2, 3);           // 6
Sum(10, 20, 30, 40);    // 100
Sum(new int[] { 5, 5 }); // 10
```

## Best Practices

✓ **Keep methods focused** - Single responsibility
✓ **Use descriptive names** - Method name describes what it does
✓ **Minimize parameters** - 3-4 is ideal, 5+ consider grouping
✓ **Use return values** - Better than output parameters
✓ **Avoid long methods** - Break into smaller methods

## Related Concepts

- [[Classes]] - Methods belong to classes
- [[Variables and Data Types]] - Parameter and return types
- [[Operators]] - Expressions within methods
- [[DRY Principle]] - Extract duplicated logic into methods