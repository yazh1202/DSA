
### Predecessor and Successor

[Link](https://www.geeksforgeeks.org/problems/predecessor-and-successor/1)

There is BST given with the root node with the key part as an integer only. You need to find the in-order **successor** and **predecessor** of a given key. If either predecessor or successor is not found, then set it to **NULL**.

**Note**:- In an inorder traversal the number just **smaller** than the target is the predecessor and the number just **greater** than the target is the successor. 

**Example 1:**

**Input:  
**      8
    /   \
   1     9
    \     \
     4    10
    /
   3  
key = 8 **Output:** 4 9 **Explanation:** In the given BST the inorder predecessor of 8 is 4 and inorder successor of 8 is 9.

# Bruteforce Approaches

1. One approach is to first get the inorder of the tree and then use it to find the successor and predecessor since it is already sorted. TC - $O(n)$ and SC-$O(n)$
2. Second approach is also to do  the inorder traversal but instead of storing all values, store only the first value greater than key and the last value smaller than key and use thme. TC remains same but SC is O(1)

## Optimal

>[!Intuition]
>Using the [[Floor and Ceil in Binary Search Tree]] technique we can determine the Floor of binary tree which would be the predecessor and ceil which would be the successor.

```python
 def findPreSuc(self, root, pre, suc, key):
        
        trav = root
        # For Predecessor
        while trav:
            val  = trav.key
            if val>=key:
                trav = trav.left
            else:
                pre = trav
                trav = trav.right
               
        # For successor 
        trav = root
        while trav:
            val  = trav.key
            if val<=key:
                trav = trav.right
            else:
                suc = trav
                trav = trav.left
```