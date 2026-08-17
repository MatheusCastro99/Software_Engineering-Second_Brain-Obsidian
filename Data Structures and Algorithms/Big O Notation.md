---
tags:
  - algorithms
  - complexity
  - data-structures
category: Data Structures and Algorithms
related: Arrays, Lists, Linked Lists, Trees
---

# Big O Notation

Big O Notation is a mathematical framework for analyzing the efficiency of algorithms by measuring how their performance scales with input size.

## What It Measures

- **Time Complexity** - How many operations an algorithm performs
- **Space Complexity** - How much additional memory an algorithm uses

## Common Complexities (Fastest → Slowest)

| Notation | Name | Example | Behavior |
|----------|------|---------|----------|
| **O(1)** | Constant | Hash table lookup | Same time regardless of input size |
| **O(log n)** | Logarithmic | Binary search | Halves problem size each step |
| **O(n)** | Linear | Simple loop | Time grows proportionally with input |
| **O(n log n)** | Linearithmic | Merge sort, Quick sort | Standard for efficient sorting |
| **O(n²)** | Quadratic | Bubble sort, nested loops | Scales poorly with large inputs |
| **O(n³)** | Cubic | Triple nested loops | Very inefficient |
| **O(2ⁿ)** | Exponential | Recursive combinations | Extremely inefficient |
| **O(n!)** | Factorial | Generating permutations | Worst case scenario |

## Visualizing Growth

For an input of 1000 items:
- O(1): 1 operation
- O(log n): ~10 operations
- O(n): 1,000 operations
- O(n log n): ~10,000 operations
- O(n²): 1,000,000 operations
- O(2ⁿ): Impossibly large number

## When to Use Each

```csharp
// O(1) - Constant time
var firstElement = array[0];
var value = dictionary["key"]; // Hash table average

// O(log n) - Binary search
int BinarySearch(int[] sorted, int target)
{
    // Divides search space in half each iteration
}

// O(n) - Linear search
for (int i = 0; i < array.Length; i++)
{
    if (array[i] == target) return i;
}

// O(n²) - Nested loops
for (int i = 0; i < array.Length; i++)
    for (int j = 0; j < array.Length; j++)
        Compare(array[i], array[j]);
```

## Key Principles

1. **Drop Constants** - O(2n) simplifies to O(n)
2. **Drop Lower-Order Terms** - O(n² + n) simplifies to O(n²)
3. **Focus on Worst Case** - Unless specified otherwise
4. **Consider Both Time AND Space** - Trade-offs often exist

## Practical Impact

Why this matters:
- Algorithm with O(n²) on 10,000 items: ~100 million operations (slow)
- Algorithm with O(n log n) on 10,000 items: ~130,000 operations (fast)
- **Choosing better algorithms matters far more than hardware upgrades**

## Related Concepts

- [[Arrays]] - Understand time complexities of array operations
- [[Linked Lists]] - Compare with arrays: O(n) access vs O(1)
- [[Trees]] - Balanced trees provide O(log n) operations
- [[Dictionaries and HashSets]] - Hash tables: O(1) average lookup