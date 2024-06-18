### Boundary Traversal of binary tree

Given a Binary Tree, find its Boundary Traversal. The traversal should be in the following order: 

1. **Left boundary nodes:** defined as the path from the root to the left-most node ie- the leaf node you could reach when you always travel preferring the left subtree over the right subtree. 
2. **Leaf nodes:** All the leaf nodes except for the ones that are part of left or right boundary.
3. **Reverse right boundary nodes:** defined as the path from the right-most node to the root. The right-most node is the leaf node you could reach when you always travel preferring the right subtree over the left subtree. Exclude the root from this as it was already included in the traversal of left boundary nodes.

**Note:** If the root doesn't have a left subtree or right subtree, then the root itself is the left or right boundary.   
  
**Example 1:**

**Input:**
        1 
      /   \
     2     3  
    / \   / \ 
   4   5 6   7
      / \
     8   9
   
**Output:** 1 2 4 8 9 6 7 3
**Explanation:**
**![](https://media.geeksforgeeks.org/wp-content/uploads/20211103204119/graph4-300x300.png)**

```python

'''
class Node:
    def __init__(self, data):
        self.right = None
        self.data = data
        self.left = None
'''
class Solution:
    # Helper method to check if the current node is leaf node or not
    def isLeaf(self,node):
        if not node.left and not node.right:
            return True
        return False
    # Getting the left part of the binary tree
    def get_left(self,root,store):
        if not root:
            return False
        if self.isLeaf(root):
            return 
        store.append(root.data)
        if root.left :
            self.get_left(root.left,store)
        else:
            self.get_left(root.right,store)
            
    # Getting the right part of the binary tree
    def get_right(self,root,store):
        if not root:
            return False
        if self.isLeaf(root):
            return 
        if root.right :
            self.get_right(root.right,store)
        else:
            self.get_right(root.left,store)
        store.append(root.data)
        
    # Getting all the leaf nodes of the binary tree
    def get_leaves(self,root,store):
        if not root:
            return
        if self.isLeaf(root):
            store.append(root.data)
            return
        self.get_leaves(root.left,store)
        self.get_leaves(root.right,store)
        
    # Combining all
    def printBoundaryView(self, root):
        
        store = [ ]
        if root:
            store.append(root.data)
        if self.isLeaf(root):
            return store
        
        # If we start from root node in all, there will be repitition
        self.get_left(root.left,store)
        self.get_leaves(root,store)
        self.get_right(root.right,store)
        
        return store

```