---
tags:
  - algorithms
  - searching
  - complexity
category: Data Structures and Algorithms
related: Big O Notation, Arrays
---

# Linear Search

Linear search checks each item in order until it finds the target.

## How it works
1. Start at the first element.
2. Compare it with the target.
3. If it matches, stop.
4. Otherwise move to the next element.
5. Repeat until found or the list ends.

## Example
```csharp
int LinearSearch(int[] numbers, int target)
{
    for (int i = 0; i < numbers.Length; i++)
    {
        if (numbers[i] == target)
            return i;
    }

    return -1;
}
```

## Complexity
- Time: O(n)
- Space: O(1)

## Use when
- Data is small
- Data is unsorted
- Simplicity is more important than speed

## Related
- [[Binary Search]]
- [[Arrays]]
- [[Big O Notation]]
