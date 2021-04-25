---
title: Trees
---
* **Depth:** How far a node is from the root. The root has a depth of 0.
* **Height:** The depth of the deepest node.
* **Binary Tree:** A tree where each node has up to 2 children.
* **Binary Search Tree:** A binary tree where all left descendents <= n < all right descendents for every node n.
* **Complete Binary Tree:** A binary tree where every level is fully filled (except maybe the last level).
* **Full Binary Tree:** A binary tree where every node has either 0 or 2 children. No nodes have only 1 child.
* **Perfect Binary Tree:** A binary tree that's both full and complete. This tree has exactly 2^height - 1 nodes.

## Traversal

### In-order traversal
Visit the left subtree, the current node, then the right subtree.
When performed on a BST, visit the nodes in ascending order.

```python
def traverse_inorder(root):
  if root:
    traverse_inorder(root.left)
    print(root)
    traverse_inorder(root.right)
```

### Pre-order traversal
Visit the current node, the left subtree, then the right subtree.
The root is always the first node visited.

```python
def traverse_preorder(root):
  if root:
    print(root)
    traverse_preorder(root.left)
    traverse_preorder(root.right)
```

### Post-order traversal
Visit the left subtree, the right subtree, then the current node.
The root is always the last node visited.

```python
def traverse_postorder(root):
  if root:
    traverse_postorder(root.left)
    traverse_postorder(root.right)
    print(root)
```

```python
# RECURSIVE
def get_height(root):
  # Base case: an empty tree has height 0.
  if not root:
    return 0
    
  # Get the height of the left and right subtrees.
  height_left = 1 + get_height(root.left)
  height_right = 1 + get_height(root.right)
  
  return max(height_left, height_right)
  
  
# ITERATIVE
def get_height(root):
  stack = []
  height = 0
  
  # Seed the stack with the root and a depth of 1.
  if root:
    stack.append((1, root))
  
  # Keep iterating as long as there are non-null nodes at the current depth.
  while stack:
    current_depth, node = stack.pop()
    
    # Update the height if current_depth > height.
    if node:
      height = max(height, current_depth)
      
      # Load the stack with nodes at the next depth.
      stack.append(1 + current_depth, node.left)
      stack.append(1 + node.right)
      
  return height
```
