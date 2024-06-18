[Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

**Input:** root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
**Output:** 3
**Explanation:** The LCA of nodes 5 and 1 is 3.

# BruteForce

>[!BruteForce :)]
>Use a search function to search the tree for each node and store the paths 
>and then find the first common point which will be the LCA.
>TC - O(2n)
>SC - O(n) - Stack Space

# Optimal

>[!Intuition]
>The intuition comes from the fact that there can be only three cases while going through the tree either we find both the nodes in the left subtree or right subtree or we can find both the nodes in the left subtree or right subtree.
>The third case is that one node is the LCA of other. We can use recursion to check for all the cases and handle them.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if not root:
            return None
	    # If either node is found then it is either the LCA or
	    # the other node is on the other side of the LCA
        if p is root or q is root:
            return root
        
        lft =  self.lowestCommonAncestor(root.left,p,q) 
        rgt =  self.lowestCommonAncestor(root.right,p,q)
        # If both nodes are on different sides of LCA then 
        # lft and rgt will return root as it is the LCA for sure
        if lft and rgt:
            return root
        # If one of the sides have both or either one of them is
        # LCA 
        return lft if not rgt else rgt
```







