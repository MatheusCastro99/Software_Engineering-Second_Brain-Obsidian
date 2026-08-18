---
tags:
  - algorithms
  - sorting
  - complexity
category: Data Structures and Algorithms
related: Big O Notation, Arrays
---

# Insertion Sort

Insertion sort builds the final sorted array one item at a time.

## How it works
1. Take the next value.
2. Compare it with the values before it.
3. Shift larger values to the right.
4. Insert the value into its proper place.
5. Repeat until the list is sorted.

## Example
```csharp
void InsertionSort(int[] numbers)
{
    for (int i = 1; i < numbers.Length; i++)
    {
        int key = numbers[i];
        int j = i - 1;

        while (j >= 0 && numbers[j] > key)
        {
            numbers[j + 1] = numbers[j];
            j--;
        }

        numbers[j + 1] = key;
    }
}
```

## Complexity
- Best case: O(n)
- Average case: O(n²)
- Worst case: O(n²)
- Space: O(1)

## Use when
- Data is nearly sorted
- Small or medium collections

## Related
- [[Bubble Sort]]
- [[Selection Sort]]
- [[Big O Notation]]
