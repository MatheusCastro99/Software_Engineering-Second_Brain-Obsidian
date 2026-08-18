---
tags:
  - data-structures
  - collections
category: Data Structures and Algorithms
related: Arrays, Lists, Linked Lists, Big O Notation
---

# Stacks and Queues

Both are linear data structures with restricted access patterns. They enforce how elements are added and removed.

## Stack (LIFO)

**Last-In-First-Out** - Like a stack of plates; last plate placed is first to remove.

### Structure
```
Push 1 → [1]
Push 2 → [1, 2]
Push 3 → [1, 2, 3] ← Top
Pop    → [1, 2]       ← Removes 3
```

### Implementation

```csharp
public class Stack<T>
{
    private List<T> items = new();
    
    // Add to top - O(1)
    public void Push(T value) => items.Add(value);
    
    // Remove from top - O(1)
    public T Pop()
    {
        if (items.Count == 0) throw new InvalidOperationException("Stack empty");
        T value = items[items.Count - 1];
        items.RemoveAt(items.Count - 1);
        return value;
    }
    
    // View top without removing - O(1)
    public T Peek() => items[items.Count - 1];
    
    // Check if empty - O(1)
    public bool IsEmpty() => items.Count == 0;
}
```

### Time Complexity

| Operation | Complexity |
|-----------|------------|
| Push | O(1) |
| Pop | O(1) |
| Peek | O(1) |
| IsEmpty | O(1) |

### Real-World Applications

- **Undo/Redo** - Store actions in stack, pop to undo
- **Browser History** - Back button uses stack
- **Function Call Stack** - How computers manage function calls
- **Expression Evaluation** - Convert infix to postfix notation
- **Backtracking** - Depth-first search algorithms

## Queue (FIFO)

**First-In-First-Out** - Like a line at a store; first person in is first to checkout.

### Structure
```
Enqueue 1 → [1]
Enqueue 2 → [1, 2]
Enqueue 3 → [1, 2, 3]
Dequeue   → [2, 3]      ← Removes 1
```

### Implementation

```csharp
public class Queue<T>
{
    private List<T> items = new();
    
    // Add to back - O(1) amortized
    public void Enqueue(T value) => items.Add(value);
    
    // Remove from front - O(n) - must shift elements
    public T Dequeue()
    {
        if (items.Count == 0) throw new InvalidOperationException("Queue empty");
        T value = items[0];
        items.RemoveAt(0); // Expensive operation
        return value;
    }
    
    // View front without removing - O(1)
    public T Peek() => items[0];
    
    // Check if empty - O(1)
    public bool IsEmpty() => items.Count == 0;
}

// Better: Use circular array or LinkedList to make Dequeue O(1)
```

### Optimal Implementation with LinkedList

```csharp
public class OptimalQueue<T>
{
    private LinkedList<T> items = new();
    
    // O(1) - Add to end
    public void Enqueue(T value) => items.AddLast(value);
    
    // O(1) - Remove from front
    public T Dequeue()
    {
        var value = items.First.Value;
        items.RemoveFirst();
        return value;
    }
    
    // O(1) - View front
    public T Peek() => items.First.Value;
}
```

### Time Complexity

| Operation | List | LinkedList |
|-----------|------|------------|
| Enqueue | O(1) | O(1) |
| Dequeue | O(n) | O(1) |
| Peek | O(1) | O(1) |
| IsEmpty | O(1) | O(1) |

### Real-World Applications

- **Print Queue** - Documents printed in order received
- **CPU Scheduling** - Processes scheduled FIFO
- **Message Queues** - Order message processing
- **Breadth-First Search (BFS)** - Traverse tree level by level
- **Load Balancing** - Distribute requests fairly

## Stack vs Queue Comparison

| Aspect | Stack | Queue |
|--------|-------|-------|
| **Order** | LIFO | FIFO |
| **Add** | Push (top) | Enqueue (back) |
| **Remove** | Pop (top) | Dequeue (front) |
| **Use Case** | Undo/Redo, DFS | Fair ordering, BFS |
| **Real World** | Stack of plates | Checkout line |

## C# Built-in Classes

```csharp
// Stack
Stack<int> stack = new Stack<int>();
stack.Push(1);
int top = stack.Pop(); // O(1) - efficient

// Queue
Queue<int> queue = new Queue<int>();
queue.Enqueue(1);
int front = queue.Dequeue(); // O(1) - efficient (LinkedList based)
```

## Related Concepts

- [[Arrays]] - Underlying storage for stacks
- [[Lists]] - Can implement both structures
- [[Linked Lists]] - Optimal for queues
- [[Big O Notation]] - Understand performance trade-offs