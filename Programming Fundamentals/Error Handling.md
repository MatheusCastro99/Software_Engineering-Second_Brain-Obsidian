---
tags:
  - fundamentals
  - error-handling
  - csharp
category: Programming Fundamentals
related: Methods, Variables and Data Types
---

# Error Handling

Error handling is the process of anticipating and gracefully managing errors that occur during program execution. Proper error handling improves reliability and user experience.

## Types of Errors

### Syntax Errors
- **Occur at** - Compile time
- **Cause** - Incorrect code structure
- **Detection** - Compiler catches before running

```csharp
// Syntax errors - won't compile
int x = 5  // Missing semicolon
if (x == 5 { } // Wrong bracket
public void Method() { // Missing return type
```

### Runtime Errors (Exceptions)
- **Occur at** - Program execution time
- **Cause** - Unexpected conditions during run
- **Examples** - Null reference, division by zero, file not found

```csharp
string text = null;
int length = text.Length; // NullReferenceException

int result = 10 / 0; // DivideByZeroException
```

### Logic Errors
- **Occur at** - Runtime (code runs but produces wrong results)
- **Cause** - Programmer mistake in algorithm
- **Example** - Off-by-one errors, wrong condition

```csharp
// Logic error: Loop never runs
for (int i = 10; i < 5; i++) { } 

// Logic error: Wrong operator
if (age => 18) { } // Should be >=
```

## Exception Handling with Try-Catch-Finally

### Basic Syntax

```csharp
try
{
    // Code that might throw exception
    int result = int.Parse("invalid");
}
catch (FormatException ex)
{
    // Handle specific exception type
    Console.WriteLine($"Invalid format: {ex.Message}");
}
catch (Exception ex)
{
    // Catch any other exception
    Console.WriteLine($"Error: {ex.Message}");
}
finally
{
    // Runs regardless - use for cleanup
    Console.WriteLine("Operation complete");
}
```

### Try Block
- Contains code that might throw an exception
- Execution stops at first exception
- Can have multiple catch blocks

### Catch Block
- Catches specific exception type
- Execute multiple catch blocks for different exceptions
- Order matters: catch most specific first

```csharp
try { }
catch (NullReferenceException) { }     // Most specific
catch (ArgumentException) { }          // Specific
catch (Exception) { }                  // General (catch-all)
catch (SystemException) { }            // Won't reach - too general
```

### Finally Block
- **Always executes** - Even if exception occurs
- **No catch needed** - Can have try-finally
- **Use for cleanup** - Close files, release resources

```csharp
try
{
    // File operation
}
finally
{
    // Close file - runs even if error occurred
    file.Close();
}
```

## Common Exception Types

| Exception | Cause | Example |
|-----------|-------|----------|
| **NullReferenceException** | Accessing null object | `null.Length` |
| **ArgumentException** | Invalid argument | `int.Parse(null)` |
| **DivideByZeroException** | Division by zero | `10 / 0` |
| **IndexOutOfRangeException** | Invalid array index | `array[100]` when size 10 |
| **FormatException** | Invalid format | `int.Parse("abc")` |
| **FileNotFoundException** | File doesn't exist | `File.ReadAllText("missing.txt")` |
| **InvalidOperationException** | Invalid operation state | `queue.Dequeue()` when empty |

## Throwing Exceptions

**Manually throw when preconditions violated**

```csharp
public void WithdrawMoney(decimal amount)
{
    if (amount <= 0)
        throw new ArgumentException("Amount must be positive");
    
    if (amount > Balance)
        throw new InvalidOperationException("Insufficient funds");
    
    Balance -= amount;
}
```

## Using Statements (Resource Management)

**Automatic cleanup when exiting scope**

```csharp
// Without using - risky
StreamReader reader = new StreamReader("file.txt");
string content = reader.ReadToEnd();
reader.Close(); // Might not run if exception occurs

// With using - safe
using (StreamReader reader = new StreamReader("file.txt"))
{
    string content = reader.ReadToEnd();
} // reader.Dispose() called automatically

// Using declaration (C# 8+)
using StreamReader reader = new StreamReader("file.txt");
string content = reader.ReadToEnd();
// Disposed automatically at end of scope
```

## Best Practices

✓ **Catch specific exceptions** - Don't catch generic `Exception`
✓ **Use finally for cleanup** - Close resources reliably
✓ **Use using for IDisposable** - Automatic cleanup
✓ **Throw early, catch late** - Fail fast, handle where appropriate
✓ **Log errors** - Don't silently fail
✗ **Don't use for control flow** - Exceptions for exceptional conditions
✗ **Don't catch and ignore** - At least log the error

```csharp
// Bad
try { result = int.Parse(input); }
catch { result = 0; } // Silent failure

// Good
try { result = int.Parse(input); }
catch (FormatException ex)
{
    Console.WriteLine($"Invalid input: {ex.Message}");
    result = 0;
}
```

## Related Concepts

- [[Variables and Data Types]] - Understand null types
- [[Methods]] - Methods throw exceptions
- [[File IO]] - Common source of exceptions