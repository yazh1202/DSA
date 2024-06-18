[653. Two Sum IV - Input is a BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)

Given the `root` of a binary search tree and an integer `k`, return `true` _if there exist two elements in the BST such that their sum is equal to_ `k`, _or_ `false` _otherwise_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/21/sum_tree_1.jpg)

**Input:** root = [5,3,6,2,4,null,7], k = 9
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/09/21/sum_tree_2.jpg)

**Input:** root = [5,3,6,2,4,null,7], k = 28
**Output:** false

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-104 <= Node.val <= 104`
- `root` is guaranteed to be a **valid** binary search tree.
- `-105 <= k <= 105`
## Bruteforce

1. Flatten the bst and then sort it and then use 2 pointer logic to solve it. TC -$O(n logn)$ and SC - $O(n)$
3. Use Inorder traversal to find inorder and then treat it as an array 2sum problem and solve it using 2 pointer logic. TC - $O(n)$ and SC - $O(n)$. 

>[!intuition]
>The intuition comes from 2 Sum problem in Arrays, from where we can observe that if we had 2 pointers over start and  end of the array the 2 Sum calculation would be easy, we use the concept of [[BST Iterator]] which would help reduce our space complexity to $O(h)$ where h is the height of tree. 
>One iterator for ascending and one for descending, while using a flag to mark the order.



```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
	# Helper for the BST traversal
    class IterBST():
        
        def __init__(self,node,reverse):
            self.stack =[]
            self.node = node
            self.reverse = reverse
            self.addMore(self.node,self.stack)

        def next(self):    
            curr = self.stack.pop()
            # Reverse referse to  descending order
            if self.reverse:
                self.addMore(curr.left,self.stack)
            else:
                self.addMore(curr.right,self.stack)
            return curr.val     

        
        def addMore(self,node,stack):
            if not node:
                return
            # For descending  we travel the right side first
            # For ascending leftside
            while node:
                stack.append(node)
                if self.reverse:
                    node = node.right
                else:
                    node = node.left
                

    def findTarget(self, root: Optional[TreeNode], k: int) -> bool:
        # ascending and descending iterator
        asc,dsc = self.IterBST(root,False),self.IterBST(root,True)
        v1,v2 = asc.next(),dsc.next()
        
        while v2>v1:
            total = v1+v2
            if total==k:
                return True
            elif total>k:
                v2 = dsc.next() 
            else:
                v1 = asc.next()

        return False

```