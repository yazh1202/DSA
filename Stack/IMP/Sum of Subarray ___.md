# Finding Sum of Minimums


```java
class Solution {
    public int sumSubarrayMins(int[] nums) {
        int[] prev = prevSmaller(nums);
        int[] next = nextSmaller(nums);    
        int mod = 1000000007;
        int n = nums.length;
        for(int i = 0;i<n;i++){
            System.out.println(prev[i]+" "+next[i]);
        }
        long ans = 0;
        for(int i = 0;i<nums.length;i++){
            int lf = i-prev[i];
            int rg = next[i]-i;
            long prod = (lf*rg)%mod;
            prod = (prod*nums[i])%mod;
            ans = (ans + prod)%mod;
        }

        return (int)ans;
            
    }
    // THis finds out the index of the element smaller than current 
    // one in the leftside
     static int[] prevSmaller(int[] nums){
        int n = nums.length;
        int[] ans = new int[nums.length];

        Stack<Integer> st = new Stack<Integer>();
        for(int i = 0;i<n;i++){
            while(!st.isEmpty()&&nums[st.peek()]>=nums[i]) st.pop();

            if(st.isEmpty()){
                ans[i] = -1;
            }else{
                ans[i] = st.peek();
            }
            st.push(i);
        }
        return ans;
    }

// THis finds out the index of the element smaller than current 
    // one in the right side
    static int[] nextSmaller(int[] nums){
        int n = nums.length;
        int[] ans = new int[nums.length];

        Stack<Integer> st = new Stack<Integer>();
        for(int i = n-1;i>=0;i--){
        // For avoiding repitition we only consider the same element subarrays once either at left or right
        
            while(!st.isEmpty()&&nums[st.peek()]>nums[i]) st.pop();

            if(st.isEmpty()){
                ans[i] = n;
            }else{
                ans[i] = st.peek();
            }
            st.push(i);
        }
        return ans;
    }
}
```


## Subarray Ranges

