
[10. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

Given a binary tree, determine if it is **height-balanced**

A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** true
> [!Intuition]
> The main intuition is that at each node if we could get the max height of the left and right subtree and compare it we can determine if the tree is balanced or not



```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        return self.recur(root)
    
    
    def recur(self,root):
        if not root:
            return True
        # Getting Max Height From each subtree
        lh = self.getHeight(root.left,0)
        rh = self.getHeight(root.right,0)
        # Checking if the difference is more than 1
        if abs(lh-rh)>1:
            return False
        # Moving on to the subtrees if current node is correct
        lft = self.recur(root.left)
        rgt = self.recur(root.right)
		# If either is not balanced the tree is not balanced
        if not lft or not rgt:
            return False
        return True
        
	# Function which returns height the max height of a binary
	# Tree Node
    def getHeight(self,root,ht):
        if not root:
            return ht
        return max(self.getHeight(root.left,ht+1),self.getHeight(root.right,ht+1))
```


# Optimized

>[!Optimisation]
>The optimsation is to use height as a tracker for the nodes and return -1 whenever the difference between the left and right subtree is more than 1
>It will recursively make sure that -1 is returned if the tree is balanced else it will return the height of the tree



```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        return not self.recur(root,0)==-1
    def recur(self,node,height):
        if not node:
            return 0
        
        lh = self.recur(node.left,height+1)
        rh = self.recur(node.right,height+1)

        if abs(lh-rh)>1 or lh==-1 or rh==-1:
            return -1

        return max(lh,rh)+1

TC - O(n)
SC - O(n)
```