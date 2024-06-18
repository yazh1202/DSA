
[101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

Given the `root` of a binary tree, _check whether it is a mirror of itself_ (i.e., symmetric around its center).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

**Input:** root = [1,2,2,3,4,4,3]
**Output:** true

>[!Intuitition]
>The basic thing is to go left for the left side and right for the right side and vice versa and keep on checking if the values are same and stop when either an asymmetry is encountered or the tree is fully traversed


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
    
        if not root:
            return 
        stack = [(root.left,root.right)]


        while stack:
            lft,rgt = stack.pop()
            # Cannot go beyond this node 
            if not lft and not rgt:
                continue
	        # Asymmetry condition 1
            if not lft or not rgt:
                return False
			# Asymmetry condition 2
            if lft.val != rgt.val:
                return False
	        # Adding to stack
            stack.append((lft.left,rgt.right))
            stack.append((lft.right,rgt.left))
        return True
            
```

