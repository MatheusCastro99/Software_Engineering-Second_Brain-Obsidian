---
tags:
  - algorithms
  - searching
  - hash-table
category: Data Structures and Algorithms
related: Dictionaries and HashSets, Big O Notation
---

# Hash Lookup

Hash lookup uses a key and a hash function to find data quickly without scanning the collection.

## How it works
1. Compute a hash for the key.
2. Use that hash to find the data bucket.
3. Check the matching key in that bucket.
4. Return the value if found.

## Example
```csharp
Dictionary<string, int> ages = new Dictionary<string, int>
{
    { "Alice", 25 },
    { "Bob", 31 }
};

Console.WriteLine(ages["Bob"]); // 31
```

## Complexity
- Average time: O(1)
- Worst case: O(n)
- Space: O(n)

## Use when
- You need fast key-based lookups
- You are using dictionaries or sets
- You want constant-time reads in most cases

## Related
- [[Dictionaries and HashSets]]
- [[Big O Notation]]
