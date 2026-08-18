---
tags:
  - algorithms
  - sorting
  - complexity
category: Data Structures and Algorithms
related: Big O Notation, Arrays
---

# Bubble Sort

Bubble sort repeatedly compares adjacent values and swaps them when they are out of order.

## How it works
1. Compare two neighboring values.
2. Swap them if the left one is larger.
3. Continue across the list.
4. Repeat until no swaps are needed.

## Example
```csharp
void BubbleSort(int[] numbers)
{
    for (int i = 0; i < numbers.Length - 1; i++)
    {
        for (int j = 0; j < numbers.Length - i - 1; j++)
        {
            if (numbers[j] > numbers[j + 1])
            {
                int temp = numbers[j];
                numbers[j] = numbers[j + 1];
                numbers[j + 1] = temp;
            }
        }
    }
}
```

## Complexity
- Time: O(n²)
- Space: O(1)

## Use when
- Learning sorting basics
- Small arrays
- Simple examples only

## Related
- [[Selection Sort]]
- [[Insertion Sort]]
- [[Big O Notation]]
