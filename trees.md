---
title: Trees
---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Definitions
* **Depth:** How far a node is from the root. The root has a depth of 0.
* **Height:** The depth of the deepest node.
* **Binary Tree:** A tree where each node has up to 2 children.
* **Binary Search Tree:** A binary tree where all left descendents <= n < all right descendents for every node n.
* **Complete Binary Tree:** A binary tree where every level is fully filled (except maybe the last level).
* **Full Binary Tree:** A binary tree where every node has either 0 or 2 children. No nodes have only 1 child.
* **Perfect Binary Tree:** A binary tree that's both full and complete. This tree has exactly 2^height - 1 nodes.

```python
class TreeNode:
  def __init__(self, val=0, left=None, right=None):
    self.val = val
    self.left = left
    self.right = right
```

## Height
### Recursive
```python
def get_height(root):
  # Base case: an empty tree has height 0.
  if not root:
    return 0
    
  # Get the height of the left and right subtrees.
  height_left = 1 + get_height(root.left)
  height_right = 1 + get_height(root.right)
  
  return max(height_left, height_right)
```

### Iterative
```python
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

## Traversal

### Depth-first
#### In-order traversal
* Visit the left subtree, the current node, then the right subtree.
* When performed on a BST, visit the nodes in ascending order.

```python
def traverse_inorder(root):
  if root:
    traverse_inorder(root.left)
    print(root.val)
    traverse_inorder(root.right)
```

#### Pre-order traversal
* Visit the current node, the left subtree, then the right subtree.
* The root is always the first node visited.

```python
def traverse_preorder(root):
  if root:
    print(root.val)
    traverse_preorder(root.left)
    traverse_preorder(root.right)
```

#### Post-order traversal
* Visit the left subtree, the right subtree, then the current node.
* The root is always the last node visited.

```python
def traverse_postorder(root):
  if root:
    traverse_postorder(root.left)
    traverse_postorder(root.right)
    print(root.val)
```

### Breadth-first
* Use a queue.

```python
import collections

def bfs_print(root):
  queue = collections.deque
  while queue:
    node = queue.popleft()
    
    print(node.val)
    
    if node.left:
      queue.append(node.left)
    if node.right:
      queue.append(node.right)
```


## Invert binary tree
Given the root of a binary tree, invert the tree and return its root.

### Recursive
```python
def invert_bt(root):
  if not root:
    return root
  
  left = invert_bt(root.left)
  right = invert_bt(root.right)
  
  root.left = right
  root.right = left
  
  return root
```

### Iterative
```python
import collections

def invert_bt(root):
  queue = collections.deque([root])
  while queue:
    node = queue.popleft()
    
    if node:
      node.left, node.right = node.right, node.left
      queue.append(node.left)
      queue.append(node.right)
    
  return root 
```

## Validate BST

### Recursive
```python
def is_valid_bst(root, low=-numpy.inf, high=numpy.inf):
  if not root:
    return True
    
  if root.val <= low or root.val >= high:
    return False
  
  return is_valid_bst(root.left, low, root.val) and is_valid_bst(root.right, root.val, high)  
```

### Iterative
```python
def is_valid_bst(root):
  stack = []
  previous = -numpy.inf
  
  while stack or root:
    while root:
      stack.append(root)
      root = root.left
      
    root = stack.pop()
    if root.val <= previous:
      return False
      
    previous = root.val
    root = root.right
    
  return True
```

## Get kth smallest element in a BST
```python
def get_kth_smallest_element(root, k):
  stack = []
  while k > 0:
    while root:
      stack.append(root)
      root = root.left
      
    root = stack.pop()
    k -= 1
    if k == 0:
      return root.val
      
    root = root.right
```
