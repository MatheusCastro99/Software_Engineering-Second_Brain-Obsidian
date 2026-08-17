---
tags:
  - data-structures
  - collections
  - csharp
category: Data Structures and Algorithms
related: Arrays, Lists, Big O Notation
---

# Dictionaries and HashSets

Both use **hash tables** for fast lookups. Dictionaries store key-value pairs; HashSets store unique values.

## Dictionary<K, V>

**Fast key-value lookup** - Averages O(1) access time.

### Structure and Purpose

A dictionary maps unique keys to values. Perfect for lookups, caching, and associations.

```csharp
// Declare
Dictionary<string, int> ages = new();

// Add
ages["Alice"] = 30;  // O(1) average
ages.Add("Bob", 25); // O(1) average

// Access
int aliceAge = ages["Alice"]; // O(1) average

// Check existence
if (ages.ContainsKey("Alice")) { } // O(1)

// Remove
ages.Remove("Bob"); // O(1) average

// Iterate
foreach (var kvp in ages) // O(n)
{
    Console.WriteLine($"{kvp.Key}: {kvp.Value}");
}
```

### Time Complexity

| Operation | Complexity | Condition |
|-----------|-----------|------------|
| Add | O(1) average | Good hash function |
| Access | O(1) average | Key exists |
| Remove | O(1) average | No collisions |
| Lookup failed | O(1) average | No collisions |
| Worst case all ops | O(n) | Many hash collisions |

### TryGetValue - Safe Access

```csharp
// Risky - throws KeyNotFoundException if missing
int age = ages["Charlie"]; // Exception!

// Safe - returns false if not found
if (ages.TryGetValue("Charlie", out int age))
{
    Console.WriteLine(age);
}
else
{
    Console.WriteLine("Key not found");
}
```

### Real-World Examples

```csharp
// Cache
Dictionary<int, string> userCache = new();
userCache[1] = "Alice";

// Config values
Dictionary<string, string> config = new()
{
    ["Database"] = "Server=localhost",
    ["Port"] = "5432"
};

// Word frequency count
Dictionary<string, int> wordCount = new();
foreach (string word in words)
{
    if (wordCount.ContainsKey(word))
        wordCount[word]++;
    else
        wordCount[word] = 1;
}

// Cleaner: Use TryGetValue
foreach (string word in words)
{
    wordCount.TryGetValue(word, out int count);
    wordCount[word] = count + 1;
}
```

## HashSet<T>

**Unique values only** - Eliminates duplicates automatically.

### Structure and Purpose

A set stores unique elements with fast membership testing. Perfect for deduplication and set operations.

```csharp
// Declare
HashSet<int> numbers = new() { 1, 2, 3, 4, 5 };

// Add - returns false if already exists
bool added = numbers.Add(6); // true
added = numbers.Add(5);      // false (already in set)

// Check membership
if (numbers.Contains(3)) { } // O(1) average

// Remove
numbers.Remove(2); // O(1) average

// Count
int size = numbers.Count; // O(1)

// Iterate
foreach (int n in numbers) { }
```

### Time Complexity

| Operation | Complexity |
|-----------|------------|
| Add | O(1) average |
| Contains | O(1) average |
| Remove | O(1) average |
| Iterate | O(n) |

### Set Operations

```csharp
HashSet<int> set1 = new() { 1, 2, 3, 4 };
HashSet<int> set2 = new() { 3, 4, 5, 6 };

// Union (combine all)
set1.UnionWith(set2);
// Result: { 1, 2, 3, 4, 5, 6 }

// Intersection (common elements)
set1.IntersectWith(set2);
// Result: { 3, 4 }

// Difference (in first but not second)
set1.ExceptWith(set2);
// Result: { 1, 2 }

// Symmetric difference (in either but not both)
set1.SymmetricExceptWith(set2);
// Result: { 1, 2, 5, 6 }
```

### Real-World Examples

```csharp
// Deduplicate
HashSet<string> uniqueEmails = new(emailList);

// Check if user visited page
HashSet<int> visitedPages = new();
if (!visitedPages.Contains(pageId))
{
    visitedPages.Add(pageId);
    // First time visiting
}

// Find common interests between users
HashSet<string> aliceInterests = new() { "sports", "music", "art" };
HashSet<string> bobInterests = new() { "music", "movies", "art" };
aliceInterests.IntersectWith(bobInterests);
// Result: { "music", "art" }
```

## Dictionary vs HashSet

| Aspect | Dictionary | HashSet |
|--------|-----------|----------|
| **Stores** | Key-value pairs | Single values |
| **Lookup** | By key | By value (membership) |
| **Duplicates** | Keys unique, values can repeat | All unique |
| **Use Case** | Mapping, caching | Deduplication, membership |
| **Example** | `<UserId, User>` | `<Unique IDs>` |

## Hash Collisions

**When different keys hash to same slot**

- Good implementation handles via chaining or probing
- Degrades to O(n) in worst case but rare
- That's why average case is O(1)

```csharp
// Example: Poor hash function
// If many keys hash to same slot, operations slow down
Dictionary<string, int> dict = new();
dict["abc"] = 1;  // Hash slot 5
dict["bca"] = 2;  // Also hash slot 5 (collision!)
dict["cab"] = 3;  // Also hash slot 5 (collision!)
// Operations on these 3 keys approach O(n)
```

## Related Concepts

- [[Arrays]] - Underlying hash table structure
- [[Lists]] - Alternative for ordered unique values
- [[Big O Notation]] - Understand performance
- [[Error Handling]] - KeyNotFoundException