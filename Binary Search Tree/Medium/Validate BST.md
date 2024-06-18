[98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

Given the `root` of a binary tree, _determine if it is a valid binary search tree (BST)_.

A **valid BST** is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

**Input:** root = [2,1,3]
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

**Input:** root = [5,1,4,null,null,3,6]
**Output:** false
**Explanation:** The root node's value is 5 but its right child's value is 4.

>[!intuition for Bruteforce]
>The inorder traversal of any BST gives a sorted order of nodes. So do that and check if the inorder traversal is sorted or not.
>P.S -> Use Iteration to save stack space and use variable to track previous value to determine sorted or not.




```python 

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:

        prev = -float("infinity")
        stack = []
        curr = root

        # Inorder traversal
        while stack or curr:

            if curr:
                stack.append(curr)
                curr = curr.left
            else:
		        
                back = stack.pop()
                # Checking if sorted or not
                if prev>=back.val:
                    return False
                else:
                    prev = back.val
                
                if back.right:
                    curr = back.right
        # Else moving on
        return True
```

>[!!SACE]


>[!Intuition for Optimal]
>The optimal traversal utilises that each node in the BST must lie withing some range defined by its parent node and if it is not within that range it is not a BST.


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:

        prev = -float("infinity")
        stack = []
        curr = root

        # Inorder traversal
        while stack or curr:

            if curr:
                stack.append(curr)
                curr = curr.left
            else:
                back = stack.pop()
                if prev>=back.val:
                    return False
                else:
                    prev = back.val
                if back.right:
                    curr = back.right
        return True 
```