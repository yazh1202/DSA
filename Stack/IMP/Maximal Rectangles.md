Given a rows x cols binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

 

Example 1:
![[Pasted image 20240208130657.png]]

Input: matrix = ["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]

Output: 6
Explanation: The maximal rectangle is shown in the above picture.

```java
	class Solution {
    public int maximalRectangle(char[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        int[] store = new int[n];
        int ans = 0;
        for(int i = 0;i<m;i++){
            for(int j = 0;j<n;j++){
                if(matrix[i][j]=='0') store[j] = 0;
                else store[j]+=1;
            }
            System.out.println(ans);
            ans = Math.max(ans,findMax(store));
        }
        return ans;
    }
	// Using the method in Histogram problem and imagining each row as a histogram of given height, rectangularity is ensured by same height
      static int findMax(int[] arr){
          //  Monotonically decreasing looking from the top
        Stack<Integer> st =  new Stack<>();
        int n = arr.length;
        int ans = 0;
        for(int i = 0;i<=n;i++){
            while(!st.isEmpty()&&(i==n||arr[st.peek()]>=arr[i])){
                int curr = arr[st.pop()];           
                int width = st.isEmpty()?i:i-st.peek()-1;
                ans = Math.max(curr*width,ans);
            }
            st.push(i);
        }
        return ans;
    }
}
```