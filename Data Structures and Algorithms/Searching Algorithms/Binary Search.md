---
tags:
  - algorithms
  - searching
  - complexity
category: Data Structures and Algorithms
related: Big O Notation, Arrays
---

# Binary Search

Binary search works only on sorted data. It cuts the search space in half each time.

## How it works
1. Find the middle item.
2. Compare it with the target.
3. If the target is smaller, search the left half.
4. If the target is larger, search the right half.
5. Repeat until found or no items remain.

## Example
```csharp
int BinarySearch(int[] sortedNumbers, int target)
{
    int left = 0;
    int right = sortedNumbers.Length - 1;

    while (left <= right)
    {
        int middle = left + (right - left) / 2;

        if (sortedNumbers[middle] == target)
            return middle;

        if (sortedNumbers[middle] < target)
            left = middle + 1;
        else
            right = middle - 1;
    }

    return -1;
}
```

## Complexity
- Time: O(log n)
- Space: O(1)

## Use when
- The data is sorted
- You need fast repeated searches

## Related
- [[Linear Search]]
- [[Arrays]]
- [[Big O Notation]]
