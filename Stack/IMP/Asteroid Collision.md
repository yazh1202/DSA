
## Lots of Edge cases is the problem
```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Stack<Integer> st = new Stack<>();
        int n = asteroids.length;        
        for(int i = 0;i<n;i++){
            int a = asteroids[i];
            // Empty or not meeting case
            if(st.isEmpty()||!meeting(st.peek(),a)) {
                st.push(a);
            }else{
                // Meeting case
                int b = Math.abs(a);

                boolean flag = false;
                // If it is lesser then the stack keeps being destroyed 
                while(!st.isEmpty()&&meeting(st.peek(),a)&&Math.abs(st.peek())<=b) {
                    int t = st.pop();
                    if(t==b){
                        flag = true;
                        break;
                    }
                }
                // If the stack top is greater the asteroid is destroyed
                //Always make sure that they are going to meet....
                if(!st.isEmpty()&&meeting(st.peek(),a)&&b<Math.abs(st.peek())) continue;

                if(!flag) st.push(a);
            }
        }
        int ind = st.size()-1;
        int[] ans = new int[st.size()];
        while(!st.isEmpty()) ans[ind--] = st.pop();
        return ans;
    }
    static boolean meeting(int a,int b){
        if(a>0&&b<0) return true;
        return false;
    }
}
```