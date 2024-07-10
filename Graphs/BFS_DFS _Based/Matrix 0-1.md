
[542. 01 Matrix](https://leetcode.com/problems/01-matrix/)

Given an `m x n` binary matrix `mat`, return _the distance of the nearest_ `0` _for each cell_.

The distance between two adjacent cells is `1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/04/24/01-1-grid.jpg)

**Input:** mat = [[0,0,0],[0,1,0],[0,0,0]]
**Output:** [[0,0,0],[0,1,0],[0,0,0]]

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/04/24/01-2-grid.jpg)

**Input:** mat = [[0,0,0],[0,1,0],[1,1,1]]
**Output:** [[0,0,0],[0,1,0],[1,2,1]]


>[!Intuition]
>The main intuition comes from [[Flood Fill]] algorithm where we had to find the matching neighbours, here instead of that we find the closest ones and then calculate their distances based on shared distance sum.



```python
from collections import deque
class Solution:
    def updateMatrix(self, mat: List[List[int]]) -> List[List[int]]:
        # Using BFS 
        m,n = len(mat),len(mat[0])
        
        # To track visited cells
        visited = [[0]*n for i in range(0,m)]
        ans = [[0]*n for i in range(0,m)]

        # Getting all the initial ones
        stack = deque()
        
        for i in range(0,m):
            for j in range(0,n):
                if mat[i][j]==0:
                    stack.append((i,j,0))
                    visited[i][j] = 1

        while stack:
            x,y,dist = stack.popleft()

            # Distance for the top cell is now known
            ans[x][y] = dist

            # Traversing all directions
            dirx = [0,1,-1,0]
            diry = [1,0,0,-1]

            for i in range(0,4):
                nx,ny = x+dirx[i],y+diry[i]

                if nx>=0 and nx<m and ny>=0 and ny<n and visited[nx][ny]==0:
                    visited[nx][ny] = 1
                    stack.append((nx,ny,dist+1))
                    


        return ans

```