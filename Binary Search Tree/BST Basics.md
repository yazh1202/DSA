# Properties

Each node has :
- Its left subtree containing values lesser than it
- Its right subtree containing values greater than it

This is true for each node in the BST.

## Handling Duplicates

There are following methods to handle duplicates

1. Make the node a pair instance storing frequency and the node value itself
2. Make the condition as  node.left<=node<node.right 
