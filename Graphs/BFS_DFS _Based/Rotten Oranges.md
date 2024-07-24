
[994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)

Solved

Medium

Topics

Companies

You are given an `m x n` `grid` where each cell can have one of three values:

- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return _the minimum number of minutes that must elapse until no cell has a fresh orange_. If _this is impossible, return_ `-1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/16/oranges.png)

**Input:** grid = [[2,1,1],[1,1,0],[0,1,1]]
**Output:** 4

**Example 2:**

**Input:** grid = [[2,1,1],[0,1,1],[1,0,1]]
**Output:** -1
**Explanation:** The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.

**Example 3:**

**Input:** grid = [[0,2]]
**Output:** 0
**Explanation:** Since there are already no fresh oranges at minute 0, the answer is just 0.

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 10`
- `grid[i][j]` is `0`, `1`, or `2`.


## Brute Force

> [!Intuition]
> Keep track of total number of oranges converted and the number of matrix converted in each traversal of the matrix as well as initial number of fresh oranges, if the total converted becomes equal to that of number of turns then return the number of minutes which will be equal to that of the number of times the matrix is traversed, if conversions in current turn is 0 and total is not equal to fresh then return -1.




```python
class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        minutes = 0
        m,n = len(grid),len(grid[0])
        fresh,total = 0,0
        for i in range(0,m):
            for j in range(0,n):
                if grid[i][j]==1:
                    fresh+=1
        
        if fresh==0:
            return 0

        while True:
            converted = 0
            current = []
            for i in range(0,m):
                for j in range(0,n):
                    if grid[i][j]==0 or grid[i][j]==2:
                        continue
                    # Marker
                    found = False
                    
					# Checking all neighbors
                    if i-1>=0 and grid[i-1][j]==2:
                        found = True
                    if j-1>=0 and grid[i][j-1]==2:
                        found = True
                    if i+1<m and grid[i+1][j]==2:
                        found = True
                    if j+1<n and grid[i][j+1]==2:
                        found = True
                    # Adding to conversion list
                    if found:
                        current.append((i,j))
                        converted+=1
            
            total+=converted
            
            if total == fresh:
                return minutes+1
            elif converted == 0:
                break
            else:
                minutes += 1
            # Marking all the converted to 2
            for j,k in current:
                grid[j][k] = 2
        
        return -1

```

>[!tip]
>Time Complexity is $O(t*n*m)$ where t is minimum time for maximum rotten oranges
>Space Complexity is $O(n)$


## Using BFS

>[!Intuition] Intuition
>In the brute force we are approaching from every cell and trying to find if it will be rotten in the current time or not, instead we can approach from the perspective of rotten oranges at each turn and calculate how many oranges will it rotten at each turn using BFS technique, then we can find out if either all oranges are rotten or we cannot rotten any more oranges, we return the time if it is former and -1 if it is latter.

```python
from collections import deque
class Solution:

    def orangesRotting(self, grid: List[List[int]]) -> int:
        m,n = len(grid),len(grid[0])
        fresh = 0
        max_time = 0

        dq = deque()
        visited = [[0]*n for i in range(0,m)]
        
        for i in range(0,m):
            for j in range(0,n):
            # Keeping track of allthe number of oranges fresh 
            # and inserting rotten one's indices into the queue
                if grid[i][j]==1:
                    fresh+=1
                elif grid[i][j] == 2:
                    visited[i][j] = 2
                    dq.append((i,j,0))
		# All possible neighbor directions
        dx = [0,-1,0,1]
        dy = [-1,0,1,0]        
        
        while dq:
	        # We don't need to care about the current level 
	        # thus we can just keep on popping in FIFO manner
            curr = dq.popleft()
            x,y,t = curr[0],curr[1],curr[2]
            max_time = t
            
            for i in range(0,4):
                n_row = x+dx[i]
                n_col = y+dy[i]
				# Cross checking if it is valid
                if n_row>=0 and n_row<m and n_col>=0 and n_col<n and visited[n_row][n_col] != 2 and grid[n_row][n_col] == 1: 
                # Marking fresh and visited 
                # Also adding next rotten orange index to dq
                    visited[n_row][n_col] = 2
                    fresh-=1
                    dq.append((n_row,n_col,t+1))
        
        # Returning max_time if all are rotten otherwise -1
        return max_time if fresh==0 else -1


```

**Time Complexity: **  $O ( n^2) x 4$


**Reason:** Worst-case - We will be making each fresh orange rotten in the grid and for each rotten orange will check in 4 directions

**Space Complexity: $O ( n ^ 2 )**$

