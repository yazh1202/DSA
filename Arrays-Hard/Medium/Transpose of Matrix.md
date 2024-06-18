
[Transpose](https://www.geeksforgeeks.org/program-to-find-transpose-of-a-matrix/)
Related Problem -  [Rotate by 90](https://leetcode.com/problems/rotate-image/submissions/1094197644/)
```java
// The important part here is the i+1, which ensures that there are 
// the swaps only occur once and not twice, which would lead to the // same array
for(int i = 0;i<m;i++){
            for(int j=i+1;j<n;j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
```
```