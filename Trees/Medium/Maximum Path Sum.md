[124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return _the maximum **path sum** of any **non-empty** path_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg)

**Input:** root = [1,2,3]
**Output:** 6

>[!Intuition]
>The main intuition is that at any node the maximum path sum will be equal to that node sum + the maximum sum we get from its left and right 
>(Umbrella shaped sum) but for each sub node we can only take either left or right subtree of it as we cannot travel any node twice.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
    # Starting from -infinity for handling all negative tree 
    
        maxs = [-float("infinity")]
        self.recur(root,maxs)
        return maxs[0]
        
    def recur(self,root,maxs):

        if not root:
            return 0

        lmax = max(self.recur(root.left,maxs),0)
        rmax = max(self.recur(root.right,maxs),0)

        # The max umbrella path for current node
        maxs[0] = max(maxs[0],lmax+rmax+root.val)

        # The umbrella path that the above node should take to maximise its own path sum
        return max(lmax,rmax)+root.val
```