
[Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

Given the `root` of a binary search tree, and an integer `k`, return _the_ `kth` _smallest value (**1-indexed**) of all the values of the nodes in the tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg)

**Input:** root = [3,1,4,null,2], k = 1
**Output:** 1

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg)

**Input:** root = [5,3,6,2,4,null,null,1], k = 3
**Output:** 3

**Constraints:**

- The number of nodes in the tree is `n`.
- `1 <= k <= n <= 104`
- `0 <= Node.val <= 104`


>[!intuition]
>For any problem that asks for the kth smallest or largest sorting the data structure is the method, for BST this can be optimised using Inorder Traversal which will take O(n) space.



# Using Inorder Traversal and Space

```python
 def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        stack = []
        inorder = []
        curr = root
        while stack or curr:
            if curr:
                stack.append(curr)
                curr = curr.left
            else:
                nxt = stack.pop()
                inorder.append(nxt.val)
                if nxt.right:
                    curr = nxt.right
	    # Since k is 1 indexed
        return inorder[k-1]
```
## Using Recursion
```python
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        ans = [0,0] #This is needed for persistence
        self.inorder(root,ans,k)

        return ans


    def inorder(self,root,count,k):
        if not root:
            return 
        self.inorder(root.left,count,k)
        count[0]+=1
        if count[0]==k:
            count[1] = root.val
            return
        self.inorder(root.right,count,k)
```


# Using [[Morris Traversal of Binary Tree]]


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        
        # Morris Traversal

        curr = root
        count = 1
        while curr:
            # Reached the end of the left subtree
            if not curr.left:
            # Check time each time you visit a node (2nd time)
                if count==k:
                    return curr.val
                count+=1
                curr = curr.right
            else:
                prev = curr.left
                # Finding the rigthmost part of the left subtree
                # This may result in the leftmost node being considered
                # If no nodes have any right subtree 
                while prev.right and prev.right is not curr:
                    prev = prev.right
                
                # Visiting for the first time 
                if not prev.right:
                    prev.right = curr
                    curr = curr.left
                else:
                # Breaking the backlink
                    prev.right = None
                    # Check time each time you visit a node (2nd time)
                    if count==k:
                        return curr.val
                    count+=1
                    curr = curr.right
            
        return -1




```