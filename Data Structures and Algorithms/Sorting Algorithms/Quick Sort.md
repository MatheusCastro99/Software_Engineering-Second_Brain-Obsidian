---
tags:
  - algorithms
  - sorting
  - complexity
category: Data Structures and Algorithms
related: Big O Notation, Arrays
---

# Quick Sort

Quick sort picks a pivot value and partitions the list around it.

## How it works
1. Choose a pivot.
2. Move smaller values left and larger values right.
3. Recursively sort the left side and the right side.
4. Combine the results.

## Example
```csharp
void QuickSort(int[] numbers, int left, int right)
{
    if (left >= right)
        return;

    int pivot = numbers[(left + right) / 2];
    int i = left;
    int j = right;

    while (i <= j)
    {
        while (numbers[i] < pivot)
            i++;

        while (numbers[j] > pivot)
            j--;

        if (i <= j)
        {
            int temp = numbers[i];
            numbers[i] = numbers[j];
            numbers[j] = temp;
            i++;
            j--;
        }
    }

    if (left < j)
        QuickSort(numbers, left, j);

    if (i < right)
        QuickSort(numbers, i, right);
}
```

## Complexity
- Best case: O(n log n)
- Average case: O(n log n)
- Worst case: O(n²)
- Space: O(log n)

## Use when
- General-purpose sorting
- Large arrays
- Efficient in-memory sorting is needed

## Related
- [[Merge Sort]]
- [[Big O Notation]]
