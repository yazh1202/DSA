
Given below is a binary tree. The task is to print the top view of binary tree. Top view of a binary tree is the set of nodes visible when the tree is viewed from the top. For the given below tree

       1  
    /     \  
   2       3  
  /  \    /   \  
4    5  6   7

Top view will be: 4 2 1 3 7  
**Note:** Return nodes from **leftmost** node to **rightmost** node. Also if 2 nodes are outside the shadow of the tree and are at same position then consider the left ones only(i.e. leftmost).   
For ex - **1 2 3 N 4 5 N 6 N 7 N 8 N 9 N N N N N** will give **8 2 1 3** as answer. Here 8 and 9 are on the same position but 9 will get shadowed.

**Example 1:**

**Input:**
      1
   /    \
  2      3
**Output:** 2 1 3

>[!Intuition]
>The main intuition is that the nodes visible from the top will always be the nodes having no nodes above them i.e they will be the first in their level either from the left or the right.


>This will use a [[Level Order Traversal]] to travel through the tree and mark horizontal distances (-1 for left and +1 for right) which will be used as key in mapping to make sure that only the first entry is stored.





```python
from collections import deque
from sortedcontainers import SortedDict
class Solution:
    
    #Function to return a list of nodes visible from the top view 
    #from left to right in Binary Tree.

	# The pair class stores the node and the horizontal distance 
	# From the root node
    class pair:
        def __init__(self,node,hd):
            self.node = node
            self.hd = hd
            
    def topView(self,root):
        mapping = SortedDict()
        dq = deque()
        ans = []
        if not root:
            return ans
        dq.append(self.pair(root,0))
        # Level order traversal
        while dq:
            current  = dq.popleft()    
            
            # If we already have a value stored to 
            # the mapping then it is the top
            
            if not (current.hd in mapping):
                mapping[current.hd] = current.node.data
            
            # Going from the left and then to the right    
            if current.node.left:
                dq.append(self.pair(current.node.left,current.hd-1))
        if current.node.right:
                dq.append(self.pair(current.node.right,current.hd+1))
        
        for i in mapping.keys():
            ans.append(mapping[i])
        return ans

```