The **next greater element** of some element `x` in an array is the **first greater** element that is **to the right** of `x` in the same array.

You are given two **distinct 0-indexed** integer arrays `nums1` and `nums2`, where `nums1` is a subset of `nums2`.

For each `0 <= i < nums1.length`, find the index `j` such that `nums1[i] == nums2[j]` and determine the **next greater element** of `nums2[j]` in `nums2`. If there is no next greater element, then the answer for this query is `-1`.

Return _an array_ `ans` _of length_ `nums1.length` _such that_ `ans[i]` _is the **next greater element** as described above._

**Example 1:**

**Input:** nums1 = [4,1,2], nums2 = [1,3,4,2]
**Output:** [-1,3,-1]
**Explanation:** The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.

>[Main Intutition]
>The LIFO ordering starting from the right side of the array makes the stack a much better choice than the bruteforce as it ensures that the next greater element is always known. 
>
>One of the doubts I had was when I am popping am I not losing possible NGE's and that is not correct as the pop operation is performed only when the current element is greater than the top element of the stack which makes sure that for any other element on the left the NGE is either the current element or the elements before it and not after it.


```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        
        Stack<Integer> st = new Stack<>();
        int[] ans = new int[nums1.length];
        HashMap<Integer,Integer> hm = new HashMap<>();
        st.push(-1);
        
        int m = nums1.length;
        int n = nums2.length;
        int ind = m-1;

        for(int i=n-1;i>=0;i--){
            while(st.peek()!=-1&&st.peek()<nums2[i]) st.pop();
            hm.put(nums2[i],st.peek());

            st.push(nums2[i]);
        }

        for(int i=0;i<m;i++){
            ans[i] = hm.get(nums1[i]);
        }
        return ans;
    }
}
```


Given a circular integer array `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`), return _the **next greater number** for every element in_ `nums`.

The **next greater number** of a number `x` is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, return `-1` for this number.


>[**Main Intuition**]
>Assume it to be a array of twice the size and repeat the method for the first one twice


```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int n = nums.length;
        Stack<Integer> st = new Stack<>();

        for(int i = n-1;i>=0;i--){
            while(!st.isEmpty()&&st.peek()<nums[i]) st.pop();
            st.push(nums[i]);
        }
		// Why do we repeat, Bruce ?
        int[] ans = new int[n];
        for(int i = n-1;i>=0;i--){
            while(!st.isEmpty()&&st.peek()<=nums[i]) st.pop();
            ans[i] = (st.isEmpty())?-1:st.peek();
            st.push(nums[i]);
        }

        return ans;
    }
}
```