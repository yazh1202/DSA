

>Not much to say about intuition as it is mere observation of the property of binary tree that the left subtree values will be lesser and right subtree values are greater.


# Ceil of BST

```python
class Solution:
    def findCeil(self,root, inp):
        prev=-1

        while root:
            if root.key>=inp:
                prev = root.key
                root = root.left
            else:
                root = root.right
                
        return prev
                
    
```

# Floor of BST


```java
public static int Floor(BinaryTreeNode<Integer> node, int input) {

		int prev = -1;

		while(node!=null){
			if (node.data==input) return input;
			if(node.data<input){
				prev= node.data;
				node = node.right;
			}
			else{
				node = node.left;
			}

		}	
		return prev; 
	}
```