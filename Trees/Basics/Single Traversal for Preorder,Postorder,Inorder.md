

> The main intuition behind this is that we take the first occurrence of the element in preorder , second occurrence in the inorder and third occurence in the postorder.
> In other words we take the node value when none of its left or right subtrees have been traversed in preorder traversal.
> For Inorder traversal we take the node value when its left subtree has been traversed and the right subtree is remaining
> For Postorder we take the node value when both the left and right subtree have been traversed.

```python
from os import *
from sys import *
from collections import *
from math import *

# Following is the Binary Tree node structure:
class BinaryTreeNode :
    def __init__(self, data) :
        self.data = data
        self.left = None
        self.right = None

def getTreeTraversal(root):
        store = [[],[],[]]
        curr = root
        prev = None
        stack = []
        
        if not root:
            return store
        while curr or stack:
           
            if curr:
                # First Appearance for the node
                # Thus we add it to our preorder
                # result
                store[1].append(curr.data)
                stack.append(curr)
                curr = curr.left
            else:
	            # Taking the top of the stack if left subtree 
	            # is exhausted
                currNode = stack[-1]
                if not currNode.right or prev!=currNode.right:
                # Inorder the condition makes sure that either 
                # the right subtree is empty or yet to be traversed
                # for the node thus we add it to inorder stack
                    store[0].append(currNode.data)
                # This condition makes us traversed the right 
                # subtree if it exists
                if currNode.right and prev!=currNode.right:
                    curr = currNode.right
                else:
	            # This will be the 3rd time visiting the node
	            # so both left and right subtrees are done 
	            # Thus we can add it into our postorder results
                    store[2].append(currNode.data)
                    stack.pop()
                    prev = currNode
        # print(store[0])

        return store
    




```

