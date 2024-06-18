
[450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return _the **root node reference** (possibly updated) of the BST_.

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/04/del_node_1.jpg)

**Input:** root = [5,3,6,2,4,null,7], key = 3
**Output:** [5,4,6,2,null,null,7]
**Explanation:** Given key to delete is 3. So we find the node with value 3 and delete it.
One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.
![](https://assets.leetcode.com/uploads/2020/09/04/del_node_supp.jpg)

**Example 2:**

**Input:** root = [5,3,6,2,4,null,7], key = 0
**Output:** [5,3,6,2,4,null,7]
**Explanation:** The tree does not contain a node with value = 0.

**Example 3:**

**Input:** root = [], key = 0
**Output:** []

>[!intuition]
>Using property of [[BST Basics|BST Basics]] itself and reassignemnt



```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
        
        # Edge cases where root is null or 
        # we have to delete the root itself
        if not root:
            return root
        if root.val == key:
            return self.delete_and_merge(root)
        
        self.search(root,key)

        return root

    # Searching for the node
    def search(self,node,key):
        if not node:
            return None
        
        if node.left and node.left.val==key:
            # If node left is the one to delete 
            # we will delete it and merge back and return
            # new replacement
            node.left = self.delete_and_merge(node.left)
            return 
        
        if node.right and node.right.val==key:
            # Same if right node is the one to delete
            node.right = self.delete_and_merge(node.right)
            return 
        
        if node.val>key:
            self.search(node.left,key)
        else:
            self.search(node.right,key)

    def delete_and_merge(self,node):
        # If the to_be_deleted node has either no left or no right
        # we return which is present
        if not node.left:
            return node.right
        if not node.right:
            return node.left

        # if both are present then
        # we can take the rightmost node of the left side of 
        # to_be_deleted and point the right side of the
        # to_be _deleted to the it. 
        curr_right = node.right
        right_most = self.get_rightmost(node.left)
        right_most.right = curr_right

        return node.left
    # helper to get rightmost side of a node
    def get_rightmost(self,node):
        while node.right:
            node = node.right
        return node


        
```