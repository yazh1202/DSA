
[543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

Given the `root` of a binary tree, return _the length of the **diameter** of the tree_.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

**Input:** root = [1,2,3,4,5]
**Output:** 3
**Explanation:** 3 is the length of the path [4,2,1,3] or [5,2,1,3].

>[!Intuition]
>The main intuition is that the longest path from any node is the sum of the 
>max depths of left subtree and right subtree


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
	    # Using array for reference storage purpose
        ans = [0]
        self.getHeight(root,0,ans)
        return ans[0]
    
    def getHeight(self,root,ht,ans):
        if not root:
            return 0
       
        lft = self.getHeight(root.left,ht+1,ans)
        rgt = self.getHeight(root.right,ht+1,ans)
        
        ans[0] = max(ans[0],abs(lft+rgt))
        
        return max(lft,rgt)+1
	        
```