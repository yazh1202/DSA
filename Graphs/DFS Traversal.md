
You are given a connected undirected graph. Perform a Depth First Traversal of the graph.  
**Note:** Use the recursive approach to find the DFS traversal of the graph starting from the 0th vertex from left to right according to the graph.

  
**Example 1:**

**Input:** V = 5 , adj = [[2,3,1] , [0], [0,4], [0], [2]]
![](https://media.geeksforgeeks.org/img-practice/graph-1659528381.png)
**Output:** 0 2 4 3 1
**Explanation**: 
0 is connected to 2, 3, 1.
1 is connected to 0.
2 is connected to 0 and 4.
3 is connected to 0.
4 is connected to 2.
so starting from 0, it will go to 2 then 4,
and then 3 and 1.
Thus dfs will be 0 2 4 3 1.

**Example 2:**

**Input:** V = 4, adj = [[1,3], [2,0], [1], [0]]
![](https://media.geeksforgeeks.org/img-practice/graph(1)-1659528893.png)
**Output:** 0 1 2 3
**Explanation**:
0 is connected to 1 , 3.
1 is connected to 0, 2. 
2 is connected to 1.
3 is connected to 0. 
so starting from 0, it will go to 1 then 2
then back to 0 then 0 to 3
thus dfs will be 0 1 2 3. 


>[!tip] Algorithm
>1. Initialise two arrays of size v to store the dfs traversal and visited array.
>2. First we add the current node to the ans and mark it as visited and then travel for each neighbor for root node and call the recursive function on it.
>3. This will make the new node the root for the next function call, and we will keep on repeating for the steps for each neighbor for each node if it is not visited during previous recursive calls.
>4. This will make the DFS Traversal complete when all nodes will be visited.


```java
	class Solution {
    // Function to return a list containing the DFS traversal of the graph.
    public ArrayList<Integer> dfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        ArrayList<Integer> ans = new ArrayList<>();
        boolean[] visited = new boolean[V];
        recur(ans,0,visited,adj);
        return ans;
    }
    static void recur(ArrayList<Integer> ans,int current,boolean[] visited,ArrayList<ArrayList<Integer>> adj){
		// Notice no base case as the recursive calls will
		// stop based on visited array markign all true 
        visited[current] = true;
        ans.add(current);
        
        for(int node:adj.get(current)){
            if(!visited[node]){
                recur(ans,node,visited,adj);
            }
        }
        
    }
}
```

```python
class Solution:
    
    #Function to return a list containing the DFS traversal of the graph.
    def dfsOfGraph(self, V, adj):
        store,visited = [],[False]*(V)
        self.dfs(0,visited,store,adj)
        return store
    
    
    def dfs(self,current,visited,store,adj):
        
        visited[current] = True
        store.append(current)
        
        for node in adj[current]:
            if not visited[node]:
                self.dfs(node,visited,store,adj)
        
```

>[!Complexity] Complexity
>The time complexity is $O(V)+O(2E) ~ O(V+E)$ where V is number of vertices and E is number of edges which also represents summation of degrees.
>Space Complexity is $O(3n)~O(n)$ since we are using recursive stack space, storage space and a visited marking array as well.











