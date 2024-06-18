
[701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

You are given the `root` node of a binary search tree (BST) and a `value` to insert into the tree. Return _the root node of the BST after the insertion_. It is **guaranteed** that the new value does not exist in the original BST.

**Notice** that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return **any of them**.

>[!Intuition]
>The intuition comes from the core property of the binary tree that all the values in the left subtree must be lesser than the parent and all the values in the right subtree must be greater than the parent.
>


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def insertIntoBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        return self.recur(root,val)

    def recur(self,node,val):
    # Will keep returning the given node till we reach 
    # a null and in that case it will return a new node which
    # will be assigned to the left/right of the parent
    # This assignment will take place for all recursively
        if not node:
            return TreeNode(val)
        if node.val>val:
            node.left = self.recur(node.left,val)
        else:
            node.right =  self.recur(node.right,val)
        return node
        
        


```