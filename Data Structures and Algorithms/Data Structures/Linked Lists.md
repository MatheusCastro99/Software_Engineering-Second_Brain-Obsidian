---
tags:
  - data-structures
  - linked-lists
category: Data Structures and Algorithms
related: Lists, Arrays, Big O Notation, Trees
---

# Linked Lists

A linked list is a dynamic data structure composed of nodes, where each node contains a value and a reference (pointer) to the next node. Unlike arrays, elements are not stored contiguously.

## Structure

### Node Class
```csharp
public class Node<T>
{
    public T Value { get; set; }
    public Node<T> Next { get; set; } // Reference to next node
}

public class LinkedList<T>
{
    public Node<T> Head { get; set; } // First node
}
```

### Visual Representation
```
┌─────────┐     ┌─────────┐     ┌─────────┐
│ Value: 1│────▶│ Value: 2│────▶│ Value: 3│────▶ null
│ Next ───┤     │ Next ───┤     │ Next ───┤
└─────────┘     └─────────┘     └─────────┘
  (Head)
```

## Time Complexity

| Operation | Complexity | Reason |
|-----------|-----------|--------|
| Access | O(n) | Must traverse from head |
| Insert at head | O(1) | Just update pointer |
| Insert at position | O(n) | Must traverse to position |
| Delete head | O(1) | Update head pointer |
| Delete at position | O(n) | Must find predecessor |
| Search | O(n) | Linear traversal |

## Types of Linked Lists

### Singly Linked List
- Each node points to next node only
- One-directional traversal
- Most common, least memory

### Doubly Linked List
```csharp
public class DoublyNode<T>
{
    public T Value { get; set; }
    public DoublyNode<T> Next { get; set; }
    public DoublyNode<T> Previous { get; set; }
}
```
- Each node has previous and next pointers
- Bidirectional traversal
- More memory but more flexible

### Circular Linked List
- Last node points back to first node
- No null terminator
- Use case: Round-robin scheduling

## Operations Example

```csharp
public class LinkedList<T>
{
    public Node<T> Head { get; set; }
    
    // Insert at beginning - O(1)
    public void InsertAtHead(T value)
    {
        var newNode = new Node<T> { Value = value };
        newNode.Next = Head;
        Head = newNode;
    }
    
    // Insert at end - O(n)
    public void InsertAtEnd(T value)
    {
        var newNode = new Node<T> { Value = value };
        if (Head == null) { Head = newNode; return; }
        
        var current = Head;
        while (current.Next != null) current = current.Next;
        current.Next = newNode;
    }
    
    // Delete head - O(1)
    public void DeleteHead()
    {
        if (Head != null) Head = Head.Next;
    }
    
    // Traverse - O(n)
    public void Display()
    {
        var current = Head;
        while (current != null)
        {
            Console.WriteLine(current.Value);
            current = current.Next;
        }
    }
}
```

## When to Use

✓ **Use Linked Lists when**: Frequent insertions/deletions at beginning, don't know size ahead of time
✗ **Avoid when**: Need fast random access, memory efficiency critical, simple array works

## Linked List vs Array vs List

| Operation | Array | List | Linked List |
|-----------|-------|------|-------------|
| **Access** | O(1) | O(1) | O(n) |
| **Insert at start** | O(n) | O(n) | O(1) |
| **Insert at end** | O(n) | O(1) amortized | O(n) |
| **Delete at start** | O(n) | O(n) | O(1) |
| **Memory** | Efficient | Good | More pointers |

## Related Concepts

- [[Arrays]] - Contiguous alternative
- [[Lists]] - Dynamic arrays alternative
- [[Big O Notation]] - Performance analysis
- [[Trees]] - Nodes similar to tree nodes