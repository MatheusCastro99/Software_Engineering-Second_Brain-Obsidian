---
tags:
  - algorithms
  - sorting
  - complexity
category: Data Structures and Algorithms
related: Big O Notation, Arrays
---

# Selection Sort

Selection sort finds the smallest remaining value and places it in the correct position.

## How it works
1. Assume the first unsorted item is the minimum.
2. Scan the rest of the list for a smaller value.
3. Swap the minimum into the correct position.
4. Repeat for the next unsorted section.

## Example
```csharp
void SelectionSort(int[] numbers)
{
    for (int i = 0; i < numbers.Length - 1; i++)
    {
        int minIndex = i;

        for (int j = i + 1; j < numbers.Length; j++)
        {
            if (numbers[j] < numbers[minIndex])
                minIndex = j;
        }

        int temp = numbers[i];
        numbers[i] = numbers[minIndex];
        numbers[minIndex] = temp;
    }
}
```

## Complexity
- Time: O(n²)
- Space: O(1)

## Use when
- Small collections
- You want a simple sorting pattern

## Related
- [[Bubble Sort]]
- [[Insertion Sort]]
- [[Big O Notation]]
