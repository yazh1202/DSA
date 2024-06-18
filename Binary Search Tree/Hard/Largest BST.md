
### Largest BST

Find better job opportunities this summer via Job-A-Thon Hiring Challenge!

Given a binary tree. Find the size of its largest subtree that is a Binary Search Tree.  
**Note:** Here Size is equal to the number of nodes in the subtree.

**Example 1:**

**Input:**
        1
      /   \
     4     4
   /   \
  6     8
**Output:** 1
**Explanation:** There's no sub-tree with size
greater than 1 which forms a BST. All the
leaf Nodes are the BSTs with size equal
to 1.

**Example 2:**

**Input:** 6 6 3 N 2 9 3 N 8 8 2
            6
        /       \
       6         3
        \      /   \
         2    9     3
          \  /  \
          8 8    2 **Output:** 2
**Explanation:** The following sub-tree is a
BST of size 2: 
       2
    /    \ 
   N      8

**Your Task:**  
You don't need to read input or print anything. Your task is to complete the function **largestBst()** that takes the root node of the Binary Tree as its input and returns the size of the largest subtree which is also the BST. If the complete Binary Tree is a BST, return the size of the complete Binary Tree. 

**Expected Time Complexity:** O(N).  
**Expected Auxiliary Space:** O(Height of the BST).

**Constraints:**  
1 ≤ Number of nodes ≤ 105  
1 ≤ Data of a node ≤ 106

# BruteForce

The bruteforce involves checking each node if it is a binary search tree using [[Validate BST]] method which takes $O(N)$ time and for N nodes the time complexity will reach $O(N^2)$


# Optimal Method
>[!Intuition]
>Taking from [[Validate BST]] method we can use Post order traversal to determine if the nodes at the bottom are BST or not and build on them to determine the largest BST by tracking the value range 




```python

class Solution:
    # Return the size of the largest sub-tree which is also a BST
    class NodeData:
        
        def __init__(self,size,min_val,max_val):
            self.size = size
            self.min_val = min_val
            self.max_val = max_val
  
    def largestBst(self, root):
        return self.getLargest(root).size

    def getLargest(self,node):
        if not node:
            # If no node is present the parent is automatically BST
            # Thus for left.max_val we return -infinity and right.min_val we return 
            # +infinity to make sure that the parent counts it
            return self.NodeData(0,float("infinity"),-float("infinity"))
            
        left_data = self.getLargest(node.left)
        right_data = self.getLargest(node.right)
        
        current  = node.data
        
        # print(left_data.max_val,current,right_data.min_val)
        if left_data.max_val < current and right_data.min_val > current:
            # If the node has subtrees which have values making it a BST
            # we can return the value based on those
            # subtrees for the parent node for checking
                current_data = self.NodeData(
                left_data.size + right_data.size + 1,
                min(left_data.min_val, current),
                max(right_data.max_val, current))
                
                return current_data
        
        # If it does not satisfy BST property then we ensure that no parent 
        # is considered a BST by passing left.max_val as +infinity and 
        # right.min_val as -infinity
        return self.NodeData(max(left_data.size,right_data.size),-float("infinity"),float("infinity"))       
            
```


>[!Complexity]
>The time complexity is O(n) and
>space complexity is O(1) if using morris traversal else O(n)

