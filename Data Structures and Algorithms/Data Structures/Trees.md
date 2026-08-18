---
tags:
  - data-structures
  - trees
  - hierarchical
category: Data Structures and Algorithms
related: Big O Notation, Linked Lists, Stacks and Queues
---

# Trees

A tree is a hierarchical data structure composed of nodes connected by edges. It's like an inverted family tree with a root at the top and leaves at the bottom.

## Structure

### Node Class
```csharp
public class TreeNode<T>
{
    public T Value { get; set; }
    public List<TreeNode<T>> Children { get; set; }
}
```

### Binary Tree (common variant)
```csharp
public class BinaryNode<T>
{
    public T Value { get; set; }
    public BinaryNode<T> Left { get; set; }  // Left child
    public BinaryNode<T> Right { get; set; } // Right child
}
```

### Visual Representation
```
        A (Root)
       / \
      B   C
     / \   \
    D   E   F (Leaves)
```

## Terminology

- **Root** - Top node with no parent
- **Leaf** - Node with no children
- **Parent/Child** - Hierarchical relationship
- **Sibling** - Nodes with same parent
- **Height** - Maximum distance from root to leaf
- **Depth** - Distance from root to specific node
- **Subtree** - Tree formed by any node and its descendants

## Common Tree Types

### Binary Search Tree (BST)
- Left child < parent < right child
- O(log n) search in balanced tree
- O(n) in worst case (unbalanced)

```csharp
public class BST<T> where T : IComparable
{
    public BinaryNode<T> Root { get; set; }
    
    public void Insert(T value)
    {
        if (Root == null) { Root = new BinaryNode<T> { Value = value }; }
        else InsertRecursive(Root, value);
    }
    
    private void InsertRecursive(BinaryNode<T> node, T value)
    {
        if (value.CompareTo(node.Value) < 0)
        {
            if (node.Left == null) node.Left = new BinaryNode<T> { Value = value };
            else InsertRecursive(node.Left, value);
        }
        else
        {
            if (node.Right == null) node.Right = new BinaryNode<T> { Value = value };
            else InsertRecursive(node.Right, value);
        }
    }
}
```

### Balanced Trees
- **AVL Tree** - Self-balancing, height difference ≤ 1
- **Red-Black Tree** - Balanced, used in TreeMap/TreeSet
- Maintain O(log n) even after insertions/deletions

## Traversal Techniques

### Breadth-First (Level Order)
```csharp
public void BFS()
{
    if (Root == null) return;
    
    var queue = new Queue<BinaryNode<T>>();
    queue.Enqueue(Root);
    
    while (queue.Count > 0)
    {
        var node = queue.Dequeue();
        Console.WriteLine(node.Value);
        
        if (node.Left != null) queue.Enqueue(node.Left);
        if (node.Right != null) queue.Enqueue(node.Right);
    }
}
// Output order: A, B, C, D, E, F
```

### Depth-First (Recursive)

**Preorder** (Parent, Left, Right)
```csharp
public void PreOrder(BinaryNode<T> node)
{
    if (node == null) return;
    Console.WriteLine(node.Value); // Parent first
    PreOrder(node.Left);           // Then left
    PreOrder(node.Right);          // Then right
}
// Output: A, B, D, E, C, F
```

**Inorder** (Left, Parent, Right) - **Useful for BST sorting**
```csharp
public void InOrder(BinaryNode<T> node)
{
    if (node == null) return;
    InOrder(node.Left);            // Left first
    Console.WriteLine(node.Value); // Parent
    InOrder(node.Right);           // Right last
}
// Output: D, B, E, A, C, F (sorted for BST)
```

**Postorder** (Left, Right, Parent)
```csharp
public void PostOrder(BinaryNode<T> node)
{
    if (node == null) return;
    PostOrder(node.Left);          // Left first
    PostOrder(node.Right);         // Right
    Console.WriteLine(node.Value); // Parent last
}
// Output: D, E, B, F, C, A (useful for deletion)
```

## Time Complexity

| Operation | Balanced | Unbalanced |
|-----------|----------|------------|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |
| Traverse | O(n) | O(n) |

## When to Use

✓ **Use trees when**: Hierarchical data, need fast search/insert, organizing data by relationships
✗ **Avoid when**: Simple linear collection works, traversing all elements repeatedly

## Applications

- **File Systems** - Folder hierarchies
- **Databases** - B-trees for indexing
- **DOM** - HTML/XML document structure
- **Compilers** - Abstract syntax trees
- **Game AI** - Decision trees

## Related Concepts

- [[Big O Notation]] - Understand performance
- [[Linked Lists]] - Similar node-based structure
- [[Stacks and Queues]] - Used in tree traversals