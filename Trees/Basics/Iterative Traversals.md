
>[!Intuition]
>The main intuition is that we must copy the functionality of the stack in recursion through our own stack.

[Article Link](https://www.enjoyalgorithms.com/blog/iterative-binary-tree-traversals-using-stack)

> Since preorder and inorder are tail recursive we can add the elements on first visit and second visit respectively
> 
# Preorder

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

        if not root:
            return []
        stack = []
        ans = []
        curr = root
        
        while stack or curr:
            # This means that we have not 
            # yet reached the end of the left subtree
            if curr:
                # Will append it to ans and stack 
                # and move along left
                ans.append(curr.val)
                #stack.append(curr)
                # Can avoid storing it and just store its right node
                # Since that will be needed 
                if curr.right:
	                stack.append(curr.right)
	            
                curr = curr.left
            # This means we have reached the end of the left
            # subtree and must go right now 
            else:
                prevNode = stack.pop()
                curr = prevNode.right

        return ans
```


# Inorder
We will add the element when we will visit it the 2nd time


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        

        stack = []
        ans = []
        node = root
        while stack or node:
            # Processing the left subtree
            if node:
                stack.append(node)
                node = node.left
            else:
            # The left subtree of the node on top of stack
            # Is processes so we will move to the right subtree
            # and will append its right node to the stack and 
            # append the top node to the answer
        
            # This is also the second visit of the node
                topnode = stack.pop()
                ans.append(topnode.val)
                node = topnode.right

		
        return ans

```


# PostOrder

>We will add the element when we are visiting it for the 3rd time.
>Also we will keep two copies, one for traversal of right node and another for 
>adding value 
## Using 2 Stacks


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

        if not root:
            return []
        stack = []
        rc_stack = []
        ans = []
        curr = root
        
        while stack or curr:
            # Have not reached the end of the left subtree
            if curr:
                if curr.right:
                    rc_stack.append(curr.right)
                stack.append(curr)
                curr = curr.left
            else:
            # Have reached the end of the left subtree 
                curr = stack[-1]
                # Checking if the stack_top has had its
                # Right subtree traversed or not 
                if rc_stack and rc_stack[-1] is curr.right:
                    curr = rc_stack.pop()
                else:
                # Both the right and left subtree of the stack is
                # traversed and now we must pop the element and move on
                    ans.append(curr.val)
                    stack.pop()
                    curr = None



        return ans
```


## Using 1 Stack

> The main change is that we take advantage of the fact that we only have to check if the last visited node was the right node of the top element of the stack to determine if both the subtrees are visited or not for the top element of the stack


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        
        stack,ans = [],[]
        curr,prev = root,None

        if not root:
            return ans

        while stack or curr:
            
            # Going through left subtree

            if curr:
                stack.append(curr)
                curr = curr.left
            else:
            # Checking if the right subtree is visited or not
                currNode = stack[-1]
                # This means that the right subtree is not yet visited 
                # for the top element in the stack
                if currNode.right and currNode.right!=prev:
                    curr = currNode.right
                else:
                # The right subtree is already visited and so is the left subtree
                # Thus we can just pop and append it to the ans
                    ans.append(currNode.val)
                    stack.pop()
                # This marks it as the last visited node
                    prev = currNode 
        return ans

```