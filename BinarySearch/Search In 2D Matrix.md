Medium


Q. Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg)

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n =  matrix[0].length;
        int i = 0,j=n-1;

        while(i<m&&j>=0){
            int curr = matrix[i][j];
            // If found then return
            if(curr==target) return true;
            // If target less go decreasing i.e row-wise
            if(curr>target){
                j--;
            // If target more go increasing i.e columnwise
            }else{
                i++;
            }
        }
        return false;
    }
}
```

