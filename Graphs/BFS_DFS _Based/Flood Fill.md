[733. Flood Fill](https://leetcode.com/problems/flood-fill/)

An image is represented by an `m x n` integer grid `image` where `image[i][j]` represents the pixel value of the image.

You are also given three integers `sr`, `sc`, and `color`. You should perform a **flood fill** on the image starting from the pixel `image[sr][sc]`.

To perform a **flood fill**, consider the starting pixel, plus any pixels connected **4-directionally** to the starting pixel of the same color as the starting pixel, plus any pixels connected **4-directionally** to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with `color`.

Return _the modified image after performing the flood fill_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/06/01/flood1-grid.jpg)

**Input:** image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, color = 2
**Output:** [[2,2,2],[2,2,0],[2,0,1]]
**Explanation:** From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected to the starting pixel.

**Example 2:**

**Input:** image = [[0,0,0],[0,0,0]], sr = 0, sc = 0, color = 0
**Output:** [[0,0,0],[0,0,0]]
**Explanation:** The starting pixel is already colored 0, so no changes are made to the image.

**Constraints:**

- `m == image.length`
- `n == image[i].length`
- `1 <= m, n <= 50`
- `0 <= image[i][j], color < 216`
- `0 <= sr < m`
- `0 <= sc < n`



# Using Recursion

The idea is that if I visit every cell from each cell I change color of then I will be coloring all the required cells. The visited array keeps track that I don't repeat 

```python
class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, color: int) -> List[List[int]]:
        m,n = len(image),len(image[0])

        visited = [[False]*n for i in range(0,m)]

        self.recursion(sr,sc,image[sr][sc],color,image,visited)

        return image
    
    def recursion(self,row,col,source,change,image,visited):
        
        m,n = len(image),len(image[0])
        # Out of bounds visited or not source color case 
        if row>=m or row<0 or col>=n or col<0 or visited[row][col]==True or image[row][col]!=source:
            return 
        
        visited[row][col] = True
        image[row][col] = change
        
        
		# Checking all 4 directions
        self.recursion(row-1,col,source,change,image,visited)
        self.recursion(row,col-1,source,change,image,visited)
        self.recursion(row,col+1,source,change,image,visited)
        self.recursion(row+1,col,source,change,image,visited)

```



# Using BFS

>[!Intuition]
>The intuition is similar to [[Rotten Oranges]] where we added all the source and then checked their neighbours but in this case we have a source coordinate given already and we have to check its neighbours and change it if it needs to be changed and add it to our dfs queue and repeat till we no longer have any sources left i.e queue is empty.


```python
from collections import deque
class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, color: int) -> List[List[int]]:

        dq = deque()
        m,n = len(image),len(image[0])
        source = image[sr][sc]
		
		# Source Point         
        dq.append((sr,sc))

        while dq:
            x,y = dq.popleft()

            # Since we are only adding to dq if it is 
            # to be colored we can directly change it
            
            image[x][y] = color

            # Travelling all directions
            dx = [0,-1,0,1]
            dy = [1,0,-1,0]
            
            for i in range(0,4):
                new_x,new_y = dx[i]+x,dy[i]+y
                # Checking if current is valid or not 
                if new_x>=m or new_x<0 or new_y>=n or new_y<0 or image[new_x][new_y]!=source or image[new_x][new_y]==color:
                    continue
                dq.append((new_x,new_y))
        
        
        return image
                 


```

