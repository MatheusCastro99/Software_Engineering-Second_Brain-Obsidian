---
tags:
  - data-structures
  - collections
  - csharp
category: Data Structures and Algorithms
related: Arrays, Linked Lists, Big O Notation
---

# Lists

A list is a dynamic, ordered collection of elements that can grow or shrink in size. It combines the convenience of arrays with flexibility.

## Key Characteristics

- **Dynamic Size** - Can add/remove elements at runtime
- **Zero-Indexed** - Access elements by position
- **Ordered** - Elements maintain insertion order
- **Generic** - `List<T>` works with any type
- **Memory** - Allocated on heap; size managed automatically

## Declaration and Initialization

```csharp
// Create empty list
List<int> numbers = new List<int>();

// With initial capacity
List<string> names = new List<string>(capacity: 10);

// With initializers
List<int> primes = new List<int> { 2, 3, 5, 7, 11 };
```

## Time Complexity

| Operation | Complexity | Reason |
|-----------|-----------|--------|
| Access | O(1) | Direct index lookup |
| Insert end | O(1) amortized | Usually just append |
| Insert middle | O(n) | Must shift elements |
| Delete | O(n) | Must shift elements |
| Search | O(n) | Linear scan |

## Common Operations

```csharp
List<int> list = new List<int> { 1, 2, 3, 4, 5 };

// Add
list.Add(6); // O(1) average
list.Insert(0, 0); // O(n) - shift required

// Access
int first = list[0]; // O(1)
int last = list[^1]; // O(1) - from end

// Remove
list.Remove(3); // O(n) - find and shift
list.RemoveAt(2); // O(n) - shift

// Iterate
foreach (int num in list) { } // O(n)

// Search
bool contains = list.Contains(5); // O(n)
int index = list.IndexOf(5); // O(n)

// Modify
list.Clear(); // O(n)
list.Count; // O(1) - size cached
list.Capacity; // Allocated space
```

## When to Use

✓ **Use List when**: Size unknown or changes frequently, need dynamic collection, order matters
✗ **Avoid List when**: Maximum performance needed, size known and fixed, frequent insertions/deletions in middle

## Lists vs Arrays

| Aspect | List | Array |
|--------|------|-------|
| **Size** | Dynamic | Fixed |
| **Add/Remove** | Easy | Difficult |
| **Access** | O(1) | O(1) |
| **Insert middle** | O(n) | O(n) |
| **Memory** | More overhead | Efficient |
| **Use case** | Most scenarios | Performance-critical |

## Related Concepts

- [[Arrays]] - Static alternative
- [[Linked Lists]] - Different insertion pattern
- [[Big O Notation]] - Understand performance trade-offs