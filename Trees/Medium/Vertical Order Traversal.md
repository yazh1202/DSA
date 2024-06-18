
[987. Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/)

Given the `root` of a binary tree, calculate the **vertical order traversal** of the binary tree.

For each node at position `(row, col)`, its left and right children will be at positions `(row + 1, col - 1)` and `(row + 1, col + 1)` respectively. The root of the tree is at `(0, 0)`.

The **vertical order traversal** of a binary tree is a list of top-to-bottom orderings for each column index starting from the leftmost column and ending on the rightmost column. There may be multiple nodes in the same row and same column. In such a case, sort these nodes by their values.

Return _the **vertical order traversal** of the binary tree_.

>[!Intuition]
>The intuition comes from the fact that we have to sort the nodes columnwise and then rowwise, we could use a map to store the nodes along with their row and column index and use that to sort them.




```

```
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from sortedcontainers import SortedDict
from collections import deque
class Solution:
    def verticalTraversal(self, root: Optional[TreeNode]) -> List[List[int]]:
        
        # Using Level Order Traversal and tuples

        mapping = SortedDict()
        dq = deque()
        ans = []
        # Using tuples in doublie linked list
        # to store row and column data as well
        dq.append((root,0,0))
        
        while dq:
            tp = dq.popleft()
            
            current = tp[0]
            row,col = tp[1],tp[2]
            
            if col not in mapping: 
                mapping[col] = SortedDict()
            
            if row not in mapping[col]:
                mapping[col][row] = []
            
            mapping[col][row].append(current.val)

            if current.left:
                dq.append((current.left,row+1,col-1))
            
            if current.right:
                dq.append((current.right,row+1,col+1))
        
		# The structure of the map is like this
		# col : {row1:{},row2:{}}
		# where both column and row are sorted using SortedDict
        for key in mapping.keys():
            temp_ans = []
            inner_map  = mapping[key]
            
            clt = list(inner_map.values())
			
            for inner_val in clt:
                inner_val.sort()
                temp_ans.extend(inner_val)

            ans.append(temp_ans)
            
        return ans
```

>[!Complexities]
>Time - O(n logn)
>Space - O(3n)~O(n)


# Using Preorder Traversal


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
# from collections import SortedDict
class Solution:
    def verticalTraversal(self, root: Optional[TreeNode]) -> List[List[int]]:
        
        store = {}

        self.recur(root,0,0,store)
        ans = []
        temp_ans = {}
        keyset = list(store.keys())
        keyset = sorted(keyset,key = lambda a:(a[1],a[0]))

        for i in keyset:
            
            row,col = i
            values = store[i]            
            values.sort()

            if col not in temp_ans:
                temp_ans[col] = []

            temp_ans[col].extend(values)
        
        actual_keys = list(temp_ans.keys())
        actual_keys.sort()

        for key in actual_keys:
            ans.append(temp_ans[key])

        
        return ans

    def recur(self,node,row,col,store):
        if not node:
            return

        if (row,col) not in store:
            store[(row,col)] = []

        store[(row,col)].append(node.val)

        self.recur(node.left,row+1,col-1,store)
        self.recur(node.right,row+1,col+1,store)

```


