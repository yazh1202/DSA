

>[!Intuition]
>Works on the use of threading the binary tree i.e rearranging and making links and breaking them to traverse a tree rather than using stack and using no space at all.

==The main advantage is no space usage==

## Algorithm

- Initialize the `root` as the current node `curr`.
    
- While `curr` is _not_ `NULL`, check if `curr` has a left child.
    
- If `curr` does not have a left child, print `curr` and update it to point to the node on the right of `curr`.
    
- Else, make `curr` the right child of the rightmost node in `curr`'s left subtree.
    
- Update `curr` to this left node.

# Inorder

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def MorrisTraversal(self, root: Optional[TreeNode]) -> int:
        
        # Morris Traversal

        curr = root
        inorder = []

        while curr:
            # Reached the end of the left subtree
            if not curr.left:
                inorder.append(curr.val)
                curr = curr.right
            else:
                prev = curr.left
                # Finding the rigthmost part of the left subtree
                # This may result in the leftmost node being considered
                # If no nodes have any right subtree 
                while prev.right and prev.right is not curr:
                    prev = prev.right
                
                # Visiting for the first time 
                if not prev.right:
                    prev.right = curr
                    curr = curr.left
                else:
                # Also visiting for the second time
                # Breaking the backlink
                    prev.right = None
                    inorder.append(curr.val)
                    curr = curr.right
                    
        return inorder
```


# Preorder

>[!Change]
>The only change is when to append to the answer i.e at the first meeting only

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def MorrisTraversal(self, root: Optional[TreeNode]) -> int:
        
        # Morris Traversal

        curr = root
        preorder = []

        while curr:
            # Reached the end of the left subtree
            if not curr.left:
                preorder.append(curr.val)
                curr = curr.right
            else:
                prev = curr.left
                # Finding the rigthmost part of the left subtree
                # This may result in the leftmost node being considered
                # If no nodes have any right subtree 
                while prev.right and prev.right is not curr:
                    prev = prev.right
                
                # Visiting for the first time 
                if not prev.right:
	                preorder.append(curr.val)
                    prev.right = curr
                    curr = curr.left
                else:
                # Also visiting for the second time
                # Breaking the backlink
                    prev.right = None
                    curr = curr.right
                    
        return preorder
```

