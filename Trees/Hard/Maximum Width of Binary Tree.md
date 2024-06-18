[662. Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/)

Given the `root` of a binary tree, return _the **maximum width** of the given tree_.

The **maximum width** of a tree is the maximum **width** among all levels.

The **width** of one level is defined as the length between the end-nodes (the leftmost and rightmost non-null nodes), where the null nodes between the end-nodes that would be present in a complete binary tree extending down to that level are also counted into the length calculation.

It is **guaranteed** that the answer will in the range of a **32-bit** signed integer.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/05/03/width1-tree.jpg)

**Input:** root = [1,3,2,5,3,null,9]
**Output:** 4
**Explanation:** The maximum width exists in the third level with length 4 (5,3,null,9).

>[!Intuition]
>The main intuition is from imagining it as a complete binary tree(all levels filled) and observing that the max width would be the width of the last level.
>This gives rise to [[Level Order Traversal]] which helps calculate the level width as the number of nodes in the queue at that level but since we also have to consider that nulls are also counted, we can use indexes and find differences between nodes at first and last indexes.




```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def widthOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        
        dq = deque()
        ans = 0
        dq.append((root,0))
        
        while dq:
            sz = len(dq)
            
            min_ind = dq[0][1]

            first,last = 0,0
            
            for i in range(0,sz):
                curr,ind = dq.popleft()
                # This is the point of confusion which may occur
                # It establishes the index of the children that
                # the node is having
                index = ind-min_ind
                if i==0 :
                    first = index
                if i==sz-1:
                    last = index
                
                if curr.left:
                    dq.append((curr.left,2*index+1))

                if curr.right:
                    dq.append((curr.right,2*index+2))
                
            ans = max(ans,last-first+1)

        return ans
```