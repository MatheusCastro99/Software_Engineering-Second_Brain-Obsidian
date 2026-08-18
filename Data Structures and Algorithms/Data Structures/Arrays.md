---
tags:
  - data-structures
  - arrays
  - csharp
category: Data Structures and Algorithms
related: Lists, Linked Lists, Big O Notation
---

# Arrays

An array is a fixed-size, contiguous block of memory that stores multiple elements of the same type. It's one of the most fundamental data structures in programming.

## Key Characteristics

- **Fixed Size** - Length cannot change after creation
- **Contiguous Memory** - All elements stored adjacently
- **Zero-Indexed** - First element is at index 0
- **Homogeneous** - All elements must be the same type
- **Direct Access** - O(1) lookup by index

## Declaration and Initialization

```csharp
// Declaration
int[] numbers = new int[5]; // 5-element array, initialized to default (0)

// With initializers
int[] primes = { 2, 3, 5, 7, 11 };

// Jagged array (array of arrays)
int[][] matrix = new int[3][]; // 3 rows, dynamic columns

// Multidimensional
int[,] grid = new int[3, 3]; // 3x3 matrix
```

## Time Complexity

| Operation | Complexity | Reason |
|-----------|-----------|--------|
| Access | O(1) | Direct memory calculation |
| Search | O(n) | May check every element |
| Insert | O(n) | Must shift elements |
| Delete | O(n) | Must shift elements |

## Advantages
- Simple and efficient for random access
- Memory efficient for storing many items
- Fast iteration through elements

## Disadvantages
- Fixed size (inflexible)
- Expensive insertions/deletions (require shifting)
- Memory wasted if partially filled

## Common Operations

```csharp
int[] arr = { 1, 2, 3, 4, 5 };

// Access
int first = arr[0]; // O(1)

// Iterate
foreach (int num in arr) { } // O(n)

// Search
Array.IndexOf(arr, 3); // O(n)

// Sort
Array.Sort(arr); // O(n log n)

// Resize
System.Array.Resize(ref arr, 10); // Creates new array
```

## When to Use

✓ Use arrays when you need **fast random access** and **fixed size**
✗ Avoid when size changes frequently - use [[Lists]] instead

## Related Concepts

- [[Lists]] - Dynamic alternative to arrays
- [[Linked Lists]] - Different access pattern
- [[Big O Notation]] - Understanding performance