
Graphs are **Nodes** connected by a line called as **Edge** (can be directed or undirected).
Graphs may or may not be enclosed

### Path

A path is a collection through which can be travelled through existing edges.

### Degree Of Path

Number of edges attached to a node. (Undirected)
Total degree of graph = 2 *  ***No. of edges**

For directed graphs there are two types of degrees

**In-Degree** - The number of edges coming to the node.

**Out-Degree** -  The number of edges going out from a node.


### Edge Weight

The cost of travelling through edge is called as edge weight.
If not mentioned it is 1.

# Types

## Undirected

Have a direction for edges
## Directed

Edges have directions

## Cyclic

Where we can reach the same node by passing through a cyclic path for each node.

## Acyclic

Where we can not reach the same node by passing through a cyclic path for each node.


![[Pasted image 20240514131955.png]]


>[!Trivia]
>In an undirected graph, there can be maximum n(n-1)/2 edges. We can choose to have (or not have) any of the n(n-1)/2 edges. So, total number of undirected graphs with n vertices is 2(n(n-1)/2).  

# Representation for Non Weighted

### Using Adjacency Matrix
1. Declaring 2d matrix of size = m x n where m is the node index and n is the number of nodes.
2. For each cell i,j mark it as 1 if an edge exists between i and j else mark it as 0. 
This takes $O(N^2)$ space

### Using Adjacency List

1. Create n+1 arraylists which (will store empty arraylists for now )where n is the number of nodes
2. For each arraylist add nodes which are its neighbors i.e have edges to it and vice versa
Space - $O(2*Edges)$

# Representation for Weighted

### Matrix
For matrix we mark it as weight instead of 1.

## List

Store pairs in the list instead of integer.



# Connected/Disconnected Components

Components connected via edges are connected

Disconnecet Components are not connected by edge but form part of graph.

![[Pasted image 20240515101504.png]]


Using **Visited Array** we can travel through disconnected components.

