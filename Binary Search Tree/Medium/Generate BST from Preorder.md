[1008. Construct Binary Search Tree from Preorder Traversal](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)

Given an array of integers preorder, which represents the **preorder traversal** of a BST (i.e., **binary search tree**), construct the tree and return _its root_.

It is **guaranteed** that there is always possible to find a binary search tree with the given requirements for the given test cases.

A **binary search tree** is a binary tree where for every node, any descendant of `Node.left` has a value **strictly less than** `Node.val`, and any descendant of `Node.right` has a value **strictly greater than** `Node.val`.

A **preorder traversal** of a binary tree displays the value of the node first, then traverses `Node.left`, then traverses `Node.right`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/03/06/1266.png)

**Input:** preorder = [8,5,1,7,10,12]
**Output:** [8,5,10,1,7,null,12]

**Example 2:**

**Input:** preorder = [1,3]
**Output:** [1,null,3]

>[!Intuition]
>The intuition comes from properties for BST and Preorder Traversal which state that for BST the nodes towards the left should be in a particular range dictated by parent node and for preorder traversal that that it starts from the root node followed by the left and right subtree.
>The range is used to determine whether a value lies towards the left or right of a node or whether it is out of bounds. This is similar to [[Validate BST]] Problem.
>P.S -> We only need to maintain upper bounds as we transfer the bound when we go to the right side of the node.

## Naive Solutions
1. Starting from root and checking for each node whether it lies towards left or right of current using bounds. Takes $O(n^2)$ time.
3. Sort the node to get inorder and preorder and using them to solve it.


## Optimal Solution

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def bstFromPreorder(self, preorder: List[int]) -> Optional[TreeNode]:
    # This index array is used for persistence with the index value of the array,starting from 0
        ind = [0]
        return self.recur(preorder,ind,float("infinity"))

    def recur(self,preorder,ind,bound):
	    # Base case where we go out of bounds either index
	    # or perorder value
        if ind[0]>=len(preorder) or preorder[ind[0]]>bound:
            return None
        # Will return the newnode if its under bounds and all
        # its subnodes are assigned
        root = TreeNode(preorder[ind[0]])
        ind[0]+=1
        root.left = self.recur(preorder,ind,root.val)
        root.right = self.recur(preorder,ind,bound)

        return root
```
## Optimal Solution with assignment of nodes

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def bstFromPreorder(self, preorder: List[int]) -> Optional[TreeNode]:
        # Starting from index 1 as the first element is always root
        # in preorder traversal
        root = TreeNode(preorder[0])
        self.recur(1,preorder,root,-float("infinity"),float("infinity"))
        
        return root
    
    def recur(self, ind, preorder, node, min_val, max_val):
        # Out of bounds base case
        if ind >= len(preorder):
            return ind
        
        curr = preorder[ind]
        # if the current element won't go into the left or right
        # subtree we return the index to be used for the next node
        if curr < min_val or curr > max_val:
            return ind
    
        newnode = TreeNode(curr)
        # If value is larger it goes to right side of node    
        if curr > node.val:
            node.right = newnode
            # Setting the node_min to current node value
            ind = self.recur(ind + 1, preorder, newnode, node.val, max_val)
        else:
        # Else the value lies towards the left side
            node.left = newnode
            # Setting the max value to current node value
            ind = self.recur(ind + 1, preorder, newnode, min_val, node.val)
        
        # This call makes sure that either the left or right side 
        # is filled with the next index values if possible
        return self.recur(ind, preorder, node, min_val, max_val)
```

