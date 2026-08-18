---
tags:
  - algorithms
  - sorting
  - complexity
category: Data Structures and Algorithms
related: Big O Notation, Arrays
---

# Merge Sort

Merge sort splits a list into halves, sorts each half, and then merges the results.

## How it works
1. Split the list into two halves.
2. Recursively sort both halves.
3. Merge the sorted halves into one sorted list.

## Example
```csharp
void MergeSort(int[] numbers, int left, int right)
{
    if (left >= right)
        return;

    int middle = left + (right - left) / 2;
    MergeSort(numbers, left, middle);
    MergeSort(numbers, middle + 1, right);

    Merge(numbers, left, middle, right);
}
```

## Complexity
- Time: O(n log n)
- Space: O(n)

## Use when
- Large datasets
- Predictable performance matters
- Stable sorting is needed

## Related
- [[Quick Sort]]
- [[Big O Notation]]
