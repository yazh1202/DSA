

[Problem Link](https://takeuforward.org/data-structure/set-matrix-zero/)
Solution - 
```java
    class Solution {
        public void setZeroes(int[][] matrix) {
            int m = matrix.length;
            int n = matrix[0].length;
            int col = -1;
            
            for(int i = 0;i<m;i++){
                for(int j = 0;j<n;j++){
                    if(matrix[i][j]==0){
                        if(j==0) {
                            col = 0;
                        }else{
                            matrix[0][j] = 0;    
                        }
                    matrix[i][0] = 0;
                        
                    }
                }
            }
            show(matrix);
            for(int i = 1;i<m;i++){
                for(int j = 1;j<n;j++){
                    if(matrix[i][0]==0||matrix[0][j]==0){
                    matrix[i][j] = 0;
                    }
                }
            }
            if(matrix[0][0]==0){
                for(int i = 0;i<n;i++){
                    matrix[0][i] = 0;
                }
            }
            if(col == 0){
                for(int i = 0;i<m;i++){
                    matrix[i][0] = 0;
                }
            }
        }
        static void show(int[][] arr){
            for(int i = 0;i<arr.length;i++){
                for(int j = 0;j<arr[0].length;j++){
                    System.out.print(arr[i][j]+" ");
                }
                System.out.println();
            }
        }
        static void set(int[][] mx,int i,int j,int m,int n,int val){
            // Upwards
            for(int a = i;a>=0;a--){
                if(mx[a][j]!=0){
                    mx[a][j] = val;
                }
            }
            // Downwards
            for(int a = i;a<m;a++){
                if(mx[a][j]!=0){
                    mx[a][j] = val;
                }
            }
            // Right
            for(int a = j;a<n;a++){
                if(mx[i][a]!=0){
                    mx[i][a] = val;
                }
            }
            // Left
            for(int a = j;a>=0;a--){
                if(mx[i][a]!=0){
                    mx[i][a] = val;
                }
            }
        }
    }
```