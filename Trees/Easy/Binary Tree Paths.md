[257. Binary Tree Paths](https://leetcode.com/problems/binary-tree-paths/)

Given the `root` of a binary tree, return _all root-to-leaf paths in **any order**_.

A **leaf** is a node with no children.


>[!Intuition/Solution]
>The intuition is a simple DFS which will store paths and add it when reaching leaf node, the mutability of string will make sure that the values one recursion call does not affect the other's results.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        ans = []
        path = ""
        self.recur(root,path,ans)
        return ans
	# Using a string we do no longer have reference store problem
	# i.e we do not need to delte the last value of the string
	# as same string will be passed to both left and right
    def recur(self,node,path,res):
        if not node:
            return 

        if path:
            path+="->"+str(node.val)
        else:
            path = str(node.val)
        
        if not node.left and not node.right:
            res.append(path)
            return
	    # path string in both left and right is same
        self.recur(node.right,path,res)
        # no change due to assignment property of string.
        self.recur(node.left,path,res)


```