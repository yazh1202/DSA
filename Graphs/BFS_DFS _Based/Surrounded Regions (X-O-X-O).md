
[130. Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)


You are given an `m x n` matrix `board` containing **letters** `'X'` and `'O'`, **capture regions** that are **surrounded**:

- **Connect**: A cell is connected to adjacent cells horizontally or vertically.
- **Region**: To form a region **connect every** `'O'` cell.
- **Surround**: The region is surrounded with `'X'` cells if you can **connect the region** with `'X'` cells and none of the region cells are on the edge of the `board`.

A **surrounded region is captured** by replacing all `'O'`s with `'X'`s in the input matrix `board`.

**Example 1:**

**Input:** board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]

**Output:** [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]

**Explanation:**

![](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

In the above diagram, the bottom region is not captured because it is on the edge of the board and cannot be surrounded.

>[!Intuition]
>The main intuition is similar to [[Rotten Oranges]] but here we try to find out the number of neighbours affected by the edge 'O's as we know that any 'O' connected to any edge 'O' will be affected by the 


```python 
from collections import deque

class Solution:
	
    def solve(self, board: List[List[str]]) -> None:
        m,n = len(board),len(board[0])
        stack = deque()
        visited = [[False]*n for col in range(0,m)]
        mark = [[False]*n for col in range(0,m)]
		
		# Adding all the boundary 'O's to the stack for DFS
        for i in range(0,m):
            for j in range(0,n):
                if (i==0 or i==m-1 or j==0 or j==n-1) and board[i][j]=='O':
                    print(i,j)
                    stack.append((i,j))
                    mark[i][j] = True 

		# Performing DFS on all the neighbors which meet the
		# boundary O's
		
        while stack:

            x,y = stack.popleft()
			# Directional Coordinates for moving 
            dx = [0,-1,0,1]
            dy = [-1,0,1,0]        
		
	        # Checking all the coordinates     
            for i in range(0,4):
                n_row = x+dx[i]
                n_col = y+dy[i]
			# Checking whether neighbor is an edge or 'X' 
                if n_row>=0 and n_row<m and n_col>=0 and n_col<n and board[n_row][n_col] == 'O' and not visited[n_row][n_col]:
                    visited[n_row][n_col] = True 
                    mark[n_row][n_col] = True 
                    stack.append((n_row,n_col))
        
        
	    # Finally marking all the ones which are surrounded
        for i in range(0,m):
            for j in range(0,n):
                if not mark[i][j]:
                    board[i][j] = 'X'
    
```