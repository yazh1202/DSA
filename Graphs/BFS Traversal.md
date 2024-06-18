
Given a directed graph. The task is to do Breadth First Traversal of this graph starting from 0.  
**Note:** One can move from node u to node v only if there's an edge from u to v. Find the BFS traversal of the graph starting from the 0th vertex, from left to right according to the input graph. Also, you should only take nodes directly or indirectly connected from Node 0 in consideration.

  
**Example 1:**

**Input:  
**V = 5, E = 4  
adj = {{1,2,3},{},{4},{},{}}
![](https://media.geeksforgeeks.org/img-practice/PROD/addEditProblem/700217/Web/Other/e0eb5630-5d6c-493a-9b1e-d16d40f10b01_1685086421.png)
**Output:**   
0 1 2 3 4
**Explanation**: 
0 is connected to 1 , 2 , 3.
2 is connected to 4.
so starting from 0, it will go to 1 then 2
then 3. After this 2 to 4, thus bfs will be
0 1 2 3 4.

**Example 2:**

**Input:  
**V = 3, E = 2  
adj = {{1,2},{},{}}
![](https://media.geeksforgeeks.org/img-practice/PROD/addEditProblem/700217/Web/Other/001e9e35-da68-4024-b1d3-e34944188a1e_1685086422.png)
**Output:**   
0 1 2
**Explanation**:
0 is connected to 1 , 2.
so starting from 0, it will go to 1 then 2,
thus bfs will be 0 1 2.

>[!tip] Algorithm
>- Initialise two arrays of size equal to number to store the answer and the visited marker array with size equal to that of number of vertices and a Queue
>- Start by adding the root node ( Either 0 or 1 ) to the dq and result.
>- Traverse all the neighbors of the root and add them to the answer and mark them visited and add them to the queue
>- Pop the element from the queue, that is the new root, do the same for it and use marker array to avoid revisiting 
>- Continue till the queue is empty.
>


```java
class Solution {
    // Function to return Breadth First Traversal of given graph.
    public ArrayList<Integer> bfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        ArrayList<Integer> bfs = new ArrayList<>();
        boolean[] visited = new boolean[V];
        Queue<Integer> dq = new LinkedList<>();
        
        dq.add(0);
        bfs.add(0);
        while(!dq.isEmpty()){
            int current = dq.poll();
            visited[current] = true;
            
            //  Getting all the neighbors
            for(Integer node : adj.get(current)){
                if(!visited[node]){
                    dq.add(node);   
                    bfs.add(node);
                    visited[node] = true;
                }
            }
        }
        return bfs;
    }
}

```

```python
from typing import List
from queue import Queue
class Solution:
    #Function to return Breadth First Traversal of given graph.
    def bfsOfGraph(self, V: int, adj: List[List[int]]) -> List[int]:
        ans,visited = [],[False]*(V)
        dq = Queue()
        
        ans.append(0)
        dq.put(0)
        visited[0] = True
        
        while not dq.empty():
            current = dq.get_nowait()
            
            #  Getting all the neighbors
            for node in adj[current]:
                if not visited[node]:
                    visited[node] = True
                    dq.put_nowait(node)
                    ans.append(node)
        
        return ans
```

>[!Time Complexity]
>**Expected Time Complexity:** O(V + E)  
**Expected Auxiliary Space:** O(V)
