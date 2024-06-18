
[Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/)

You are given the `root` of a binary search tree (BST), where the values of **exactly** two nodes of the tree were swapped by mistake. _Recover the tree without changing its structure_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/28/recover1.jpg)

**Input:** root = [1,3,null,null,2]
**Output:** [3,1,null,null,2]
**Explanation:** 3 cannot be a left child of 1 because 3 > 1. Swapping 1 and 3 makes the BST valid.

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/28/recover2.jpg)

**Input:** root = [3,1,4,null,null,2]
**Output:** [2,1,4,null,null,3]
**Explanation:** 2 cannot be in the right subtree of 3 because 2 < 3. Swapping 2 and 3 makes the BST valid.

**Constraints:**

- The number of nodes in the tree is in the range `[2, 1000]`.
- `-231 <= Node.val <= 231 - 1`

# Bruteforce 

For bruteforce we can first calculate the inorder traversal, sort it and then use it to reassign values for the tree.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def recoverTree(self, root: Optional[TreeNode]) -> None:
        store = []
        # First call to store inorder
        self.inorder(root,store,[-1])
        # Then sort
        store.sort()
        # Finally reassign it
        self.inorder(root,store,[0])

    def inorder(self,node,store,ind):
        if not node:
            return
        self.inorder(node.left,store,ind)
        # List because list persists
        if ind[0]!=-1:
            node.val = store[ind[0]]   
            ind[0]+=1
        else:
            store.append(node.val)
        self.inorder(node.right,store,ind)
        
```

## Optimal

>[!Intuition]
>The intuition is that we are guaranteed that only two nodes are swapped, so we can be sure if we find them during our traversal we can swap them. 
>Using inorder traversal we can keep a prev variable to track the previous value and check current one is violating the order, if it is then we take it as the second and the prev as first violator. If we find other violator we reassign second to it.
>

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def recoverTree(self, root: Optional[TreeNode]) -> None:
	    # Using list to store first,last and prev to persist with the 
	    # Recursion calls made
        swapping = []
        self.inorder(root, swapping, [None])  # Pass prev as a list

        temp = swapping[0][0].val
        swapping[0][0].val = swapping[0][1].val
        swapping[0][1].val = temp

    def inorder(self, node, swapping, prev):
        if not node:
            return
        
        self.inorder(node.left, swapping, prev)

        if prev[0] and prev[0].val > node.val:
            if swapping:
                swapping[0][1] = node
            else:
                swapping.append([prev[0], node])
        
        prev[0] = node  # Update prev directly in the list
        self.inorder(node.right, swapping, prev)

        
```
