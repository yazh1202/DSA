### Detect cycle in an undirected graph

Given an undirected graph with V vertices labelled from 0 to V-1 and E edges, check whether it contains any cycle or not. Graph is in the form of adjacency list where adj[i] contains all the nodes ith node is having edge with.**![](C:\Users\Mukul kumar\Desktop\GFG_PIC.JPG)**

**Example 1:**

**Input:**  
V = 5, E = 5
adj = {{1}, {0, 2, 4}, {1, 3}, {2, 4}, {1, 3}} 
**Output:** 1
**Explanation:** 
![](https://media.geeksforgeeks.org/img-practice/PROD/addEditProblem/700219/Web/Other/891791f9-1abb-45b1-80f2-7af46d73dcd2_1685086491.png)
1->2->3->4->1 is a cycle.

**Example 2:**

**Input:** 
V = 4, E = 2
adj = {{}, {2}, {1, 3}, {2}}
**Output:** 0
**Explanation:** 
![](https://media.geeksforgeeks.org/img-practice/PROD/addEditProblem/700219/Web/Other/d8cbd97e-406e-4f50-a38c-6a58747df876_1685086491.png)
No cycle in the graph.

**Your Task:**  
You don't need to read or print anything. Your task is to complete the function **isCycle()** which takes V denoting the number of vertices and adjacency list as input parameters and returns a boolean value denoting if the undirected graph contains any cycle or not, return 1 if a cycle is present else return 0.

**NOTE:** The adjacency list denotes the edges of the graph where edges[i] stores all other vertices to which ith vertex is connected.

**Expected Time Complexity:** O(V + E)  
**Expected Space Complexity:** O(V)

**Constraints:**  
1 ≤ V, E ≤ 105

# Using BFS

>[!Intuition]
>The main intuition is that we must not visit the same node twice and for that we track it using the visited array we usually use for BFS. Also, we make sure that we travel through all possible starting nodes in the graph handling the case where it is disconnected.

```python

class Solution:
    
    
	def isCycle(self, V: int, adj: List[List[int]]) -> bool:
	    visited = [False]*V
	    # This for loop ensures that we do not miss out on 
	    # Disconnected graphs
        for i in range(0,V):
            if not visited[i] and self.findCycle(i,visited,V,adj):
                return True
        return False
                
    #Function to detect cycle in an undirected graph.
    def findCycle(self,src, visited,V: int, adj: List[List[int]]) -> bool:
        # Marking it as True so we don't visit it again
        visited[src] = True
        stack = [(src,-1)]
        while stack:
            curr,parent = stack.pop()
            for i in adj[curr]:
                if not visited[i]:
                    visited[i] = True
                    stack.append((i,curr))
                elif i!=parent:
                    return True
        return False   
    
```


## Complexities

**Time Complexity:** O(N + 2E) + O(N), Where N = Nodes, 2E is for total degrees as we traverse all adjacent nodes. In the case of connected components of a graph, it will take another O(N) time.

**Space Complexity:** O(N) + O(N) ~ O(N), Space for queue data structure and visited array.

q