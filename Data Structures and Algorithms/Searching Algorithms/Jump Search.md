---
tags:
  - algorithms
  - searching
  - complexity
category: Data Structures and Algorithms
related: Big O Notation, Arrays
---

# Jump Search

Jump search works on sorted data by jumping ahead in blocks instead of checking every item.

## How it works
1. Pick a block size, often sqrt(n).
2. Jump forward through the list in blocks.
3. Find the block that likely contains the target.
4. Search within that block linearly.

## Example
```csharp
int JumpSearch(int[] sortedNumbers, int target)
{
    int n = sortedNumbers.Length;
    int jump = (int)Math.Sqrt(n);
    int previous = 0;

    while (previous < n && sortedNumbers[Math.Min(jump, n) - 1] < target)
    {
        previous = jump;
        jump += (int)Math.Sqrt(n);

        if (previous >= n)
            return -1;
    }

    while (previous < n && sortedNumbers[previous] < target)
    {
        previous++;
    }

    if (previous < n && sortedNumbers[previous] == target)
        return previous;

    return -1;
}
```

## Complexity
- Time: O(√n)
- Space: O(1)

## Use when
- Data is sorted
- You want a middle ground between linear and binary search

## Related
- [[Binary Search]]
- [[Linear Search]]
- [[Big O Notation]]
