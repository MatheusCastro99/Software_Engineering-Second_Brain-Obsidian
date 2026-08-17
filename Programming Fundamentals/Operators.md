---
tags:
  - fundamentals
  - csharp
  - operators
category: Programming Fundamentals
related: Variables and Data Types, Methods
---

# Operators

Operators are symbols that perform operations on variables and values. They enable expressions and computations.

## Arithmetic Operators

**Basic math operations**

```csharp
int a = 10, b = 3;

int add = a + b;       // 13 - Addition
int subtract = a - b;  // 7  - Subtraction
int multiply = a * b;  // 30 - Multiplication
int divide = a / b;    // 3  - Division (integer division)
int remainder = a % b; // 1  - Modulo (remainder)

// Increment/Decrement
int x = 5;
x++;        // 6 - Post-increment
++x;        // 7 - Pre-increment
x--;        // 6 - Post-decrement
--x;        // 5 - Pre-decrement
```

| Operator | Symbol | Example | Result |
|----------|--------|---------|--------|
| Addition | + | 10 + 3 | 13 |
| Subtraction | - | 10 - 3 | 7 |
| Multiplication | * | 10 * 3 | 30 |
| Division | / | 10 / 3 | 3 (integer) |
| Modulo | % | 10 % 3 | 1 |

## Relational Operators

**Compare values and return boolean**

```csharp
int a = 5, b = 3;

bool equal = a == b;        // false - Equal
bool notEqual = a != b;     // true  - Not equal
bool greater = a > b;       // true  - Greater than
bool greaterOrEqual = a >= b; // true  - Greater or equal
bool less = a < b;          // false - Less than
bool lessOrEqual = a <= b;  // false - Less or equal
```

| Operator | Symbol | True When | Example |
|----------|--------|-----------|----------|
| Equal to | == | Values are same | 5 == 5 |
| Not equal to | != | Values differ | 5 != 3 |
| Greater than | > | Left > right | 5 > 3 |
| Less than | < | Left < right | 3 < 5 |
| Greater or equal | >= | Left >= right | 5 >= 5 |
| Less or equal | <= | Left <= right | 5 <= 5 |

## Logical Operators

**Combine boolean conditions**

```csharp
bool isAvailable = true;
bool isAffordable = false;

// AND - Both must be true
bool canBuy = isAvailable && isAffordable; // false

// OR - At least one must be true
bool shouldInquire = isAvailable || isAffordable; // true

// NOT - Inverts boolean
bool isUnavailable = !isAvailable; // false
```

| Operator | Symbol | True When | Example |
|----------|--------|-----------|----------|
| AND | && | Both operands true | true && true |
| OR | \|\| | At least one true | true \|\| false |
| NOT | ! | Operand is false | !false |

### Truth Table

| A | B | A && B | A \|\| B | !A |
|---|---|--------|---------|----|
| T | T | T | T | F |
| T | F | F | T | F |
| F | T | F | T | T |
| F | F | F | F | T |

## Assignment Operators

**Assign and modify values**

```csharp
int x = 10;

x = 5;      // Assign: x is now 5
x += 3;     // Add and assign: x = x + 3 (8)
x -= 2;     // Subtract and assign: x = x - 2 (6)
x *= 2;     // Multiply and assign: x = x * 2 (12)
x /= 3;     // Divide and assign: x = x / 3 (4)
x %= 2;     // Modulo and assign: x = x % 2 (0)
```

| Operator | Example | Equivalent |
|----------|---------|------------|
| = | x = 5 | Assign |
| += | x += 3 | x = x + 3 |
| -= | x -= 2 | x = x - 2 |
| *= | x *= 2 | x = x * 2 |
| /= | x /= 3 | x = x / 3 |
| %= | x %= 2 | x = x % 2 |

## Ternary Operator

**Conditional expression (one-liner if/else)**

```csharp
string grade = score >= 60 ? "Pass" : "Fail";
// If score >= 60, grade = "Pass", else grade = "Fail"

int discount = isPremium ? 20 : 5;
```

**Syntax**: `condition ? valueIfTrue : valueIfFalse`

## Operator Precedence

**Order of evaluation (highest to lowest)**

1. `()` - Parentheses
2. `! ++ -- +x -x` - Logical NOT, Increment, Unary plus/minus
3. `* / %` - Multiplication, Division, Modulo
4. `+ -` - Addition, Subtraction
5. `< <= > >=` - Relational
6. `== !=` - Equality
7. `&&` - Logical AND
8. `||` - Logical OR
9. `? :` - Ternary
10. `= += -= *= /=` - Assignment

```csharp
// Precedence matters
int result1 = 2 + 3 * 4;    // 14 (multiply first)
int result2 = (2 + 3) * 4;  // 20 (parentheses first)

bool check = true && false || true; // true (AND first)
bool check2 = true && (false || true); // true
```

## Common Patterns

```csharp
// Check if in range
if (age >= 18 && age <= 65) { }

// Check string validity
if (!string.IsNullOrEmpty(name)) { }

// Complex conditions
bool isValid = (score > 90) || (extra && score > 80);

// Inverse condition
if (!(isAvailable && isAffordable)) { }
```

## Related Concepts

- [[Variables and Data Types]] - Operands are variables
- [[Methods]] - Used within method bodies