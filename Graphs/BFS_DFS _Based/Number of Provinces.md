[547. Number of Provinces](https://leetcode.com/problems/number-of-provinces/)

There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `ith` city and the `jth` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return _the total number of **provinces**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

**Input:** isConnected = [[1,1,0],[1,1,0],[0,0,1]]
**Output:** 2

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg)

**Input:** isConnected = [[1,0,0],[0,1,0],[0,0,1]]
**Output:** 3

**Constraints:**

- `1 <= n <= 200`
- `n == isConnected.length`
- `n == isConnected[i].length`
- `isConnected[i][j]` is `1` or `0`.
- `isConnected[i][i] == 1`
- `isConnected[i][j] == isConnected[j][i]`

>[!Intuition]
>It can be inferred from problem statement that we can travel from one point in the tree to any other point in a province using indirect connections, this is similar to [[DFS Traversal]] of Graphs where we travel through each neighbours depth (max number of nodes reachable (directly or indirectly) from that node) thus we can use it to determine the number of provinces.
>This can be done by running dfs for each node in the graph and using visited array

```python
class Solution:
    def findCircleNum(self, isConnected: List[List[int]]) -> int:

        
        n = len(isConnected)
        count = 0
        visited=[0]*n
        # Running for each node
        for i in range(0,n):
        # Using visited array to avoid double counting
            if visited[i]!=1:
                count+=1
                self.dfs(i,0,isConnected,visited)
            
        return count
    
	# DFS 
    def dfs(self,i,j,matrix,visited):
        visited[i] = 1
        for ind,mark in enumerate(matrix[i]):
            if visited[ind]==0 and mark==1:
                self.dfs(ind,0,matrix,visited)
        
```