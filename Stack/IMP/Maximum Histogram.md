>Intuition
>The main intuition is that for any index the maximal area rectangle will be the ranges to the left and right till which it is the minimum multiplied by its height. The Next Smaller Element Stack will give us the index till which its range ends 	
## Multi Pass Solution
```java
class Solution {
    public int largestRectangleArea(int[] ht) {
        
        Stack<Integer> st = new Stack<>();
	    // Finds the left and right smallest 
	    // for the width at each position
        int n = ht.length;
        int[] lft = new int[n];
        int[] rgt = new int[n];

        for(int i = 0;i<n;i++){
            while(!st.isEmpty()&&ht[st.peek()]>=ht[i]) st.pop();

            if(st.isEmpty()){
                lft[i] = 0; 
            }else{
            // The +1 is for marking the wall which will start from 
            // the next index
                lft[i] =  st.peek()+1;
            }
            st.push(i);
        }
        st.clear(); 
        for(int i =n-1;i>=0;i--){
            while(!st.isEmpty()&&ht[st.peek()]>=ht[i]) st.pop();

            if(st.isEmpty()){
            // The -1 is for marking the wall which will start from 
            // previous index
                rgt[i] = n-1; 
            }else{
                rgt[i] =  st.peek()-1;
            }
            st.push(i);
        }
        int ans = 0;
        for(int i = 0;i<n;i++){
           ans=Math.max((rgt[i]-lft[i]+1)*ht[i],ans);
        }
        return ans;
    }
}
```
## One pass Solution 
```java
class Solution {
    public int largestRectangleArea(int[] ht) {
        int ans = 0;
        int n = ht.length;
        Stack<Integer> st = new Stack<Integer>();

        for(int i = 0;i<=n;i++){
            while(!st.isEmpty()&&(i==n||ht[st.peek()]>=ht[i])){

                int ch = ht[st.pop()];
                int width = st.isEmpty()?i:i-st.peek()-1;
                
                ans = Math.max(ans,width*ch);
            }
            st.push(i);
        }
        return ans;
    }
}
```
