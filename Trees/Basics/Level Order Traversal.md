
[103. Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

Given the `root` of a binary tree, return _the zigzag level order traversal of its nodes' values_. (i.e., from left to right, then right to left for the next level and alternate between).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** [[3],[20,9],[15,7]]

>[!Intuition]
>The main intuition is LIFO policy which is implemented using deque and zig zag is done via an indexing trick using a boolean flag to reverse the sequence of insertion in Level Order Traversal.



```python
    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, val=0, left=None, right=None):
    #         self.val = val
    #         self.left = left
    #         self.right = right
    from queue import deque
    class Solution:
        def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
            
            dq = deque()
            dq.append(root)
            
            flag = False
            ans = []

            if not root:
                return []
            
            while dq:
                # This will tell us the nodes that are in the current level
                # Because all nodes have been added during last 
                # Traversal 
                size = len(dq)
                
                row = [0]*size
                
                for i in range(0,size):
                    curr = dq.popleft()
					# This is the only difference between
					# normal level order and zig zag
					# It defines where to fill the current element 
					# at, either from the end or from the start
                    ind = size-i-1 if flag else i
                    
                    row[ind] = curr.val

                    if curr.left :
                        dq.append(curr.left)
                    if curr.right:
                        dq.append(curr.right)
                
                ans.append(row)
                
                flag = not flag
            
            return ans
```

The time complexity of level order traversal using recursion is not as straightforward as it may seem at first glance. In the recursive approach to level order traversal, the time complexity is indeed not simply O(n), where n is the total number of nodes in the tree. The reason is that the recursive function is called for each level of the tree, and the number of calls depends on the height of the tree. Here's a more detailed explanation:

1. **Recursive Calls**: In the recursive approach, the `levelOrder` function is called for each level of the tree. The number of levels in a tree is equal to the height of the tree, which can be as high as n (in the case of a skewed tree) or as low as log n (in the case of a balanced tree).
2. **Time Complexity per Level**: Within each level, the time complexity is O(n_i), where n_i is the number of nodes at that level. This is because we visit each node exactly once at that level.
3. **Total Time Complexity**: Summing up the time complexities for each level, we get:`Time Complexity = O(n_1) + O(n_2) + ... + O(n_h)` where h is the height of the tree.
- **Worst-Case Scenario**: In the worst-case scenario, the tree is skewed, and the height of the tree is h = n. In this case, the time complexity becomes:`Time Complexity = O(n) + O(n-1) + ... + O(1) = O(n^2)`
    

- **Best-Case Scenario**: In the best-case scenario, the tree is balanced, and the height of the tree is h = log n. In this case, the time complexity becomes:`Time Complexity = O(n_1) + O(n_2) + ... + O(n_log n) = O(n)`