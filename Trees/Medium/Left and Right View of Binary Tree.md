
[199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)

Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return _the values of the nodes you can see ordered from top to bottom_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

**Input:** root = [1,2,3,null,5,null,4]
**Output:** [1,3,4]


# Using  [[Level Order Traversal]]

>[!Intuition]
>The main intuition comes from knowledge of level order traversal, through which one can observer that the left side view of the tree will always include the node encountered first during level order traversal and the right side view view include nodes encountered last during level order traversal


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        store = []
        stack = deque()
        stack.append(root)
        if not root:
            return store
        while stack:

            size = len(stack)
            for i in range(0,size):
                curr = stack.popleft()     
                   
                if curr.left:
                    stack.append(curr.left)
                if curr.right:
                    stack.append(curr.right)    
				# For left view i==0 will be used
                if i==size-1:
                    store.append(curr.val)
        
        return store
```

>[!Quote]
>Time Complexity  -  **O(N)** since we are using queue for BFS
>Space Complexity  -  **O(N)** since we are using queue

# Using DFS

>[!Intuition]
>To get the left and right view of a Binary Tree, we perform a depth-first traversal of the Binary Tree while keeping track of the level of each node. For both the left and right view, we’ll ensure that only the first node encountered at each level is added to the result vector.



```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        ans = []
        self.recur(root,ans,0)

        return ans

    def recur(self,root,store,level):

        if not root:
            return 

        # First encountered node at this level
        if level==len(store):
            store.append(root.val)
        
        # For left side view this will be reversed
        self.recur(root.right,store,level+1)
        self.recur(root.left,store,level+1)
        

```





>[!Quote]
>**Time Complexity: O(log2N)** where N is the number of nodes in the Binary Tree. This complexity arises as we travel along the height of the Binary Tree. For a balanced binary tree, the height is log2N but in the worst case when the tree is skewed, the complexity becomes O(N).
>**Space Complexity : O(log2N)** where N is the number of nodes in the Binary Tree. This complexity arises because we store the leftmost and rightmost nodes in an additional vector. The size of this result vector is proportional to the height of the Binary Tree which will be log2N when the tree is balanced and O(N) in the worst case of a skewed tree.
>1. O(H): Recursive Stack Space is used to calculate the height of the tree at each node which is proportional to the height of the tree.
>2. The recursive nature of the getHeight function, which incurs space on the call stack for each recursive call until it reaches the leaf nodes or the height of the tree
