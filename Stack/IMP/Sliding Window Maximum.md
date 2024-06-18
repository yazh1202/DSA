You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3
**Output:** [3,3,5,5,6,7]
**Explanation:** 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       **3**
 1 [3  -1  -3] 5  3  6  7       **3**
 1  3 [-1  -3  5] 3  6  7      ** 5**
 1  3  -1 [-3  5  3] 6  7       **5**
 1  3  -1  -3 [5  3  6] 7       **6**
 1  3  -1  -3  5 [3  6  7]      **7**

**Example 2:**

**Input:** nums = [1], k = 1
**Output:** [1]


```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        LinkedList<Integer> ll = new LinkedList<>();
        int n = nums.length;
        int[] ans = new int[n-k+1];
        int ind = 0;
        for(int i = 0;i<n;i++){
            // Removing out of bounds
            while(!ll.isEmpty()&&ll.getFirst()==i-k) ll.removeFirst();

            // New ones to be added to the end of the linked
            // The newer element will always be compared to the last added one at the end
          while(!ll.isEmpty()&&nums[ll.getLast()]<=nums[i]) ll.removeLast();

            ll.addLast(i);

            if(i>=k-1) ans[ind++] = nums[ll.getFirst()];
            
        }
        return ans;
    }
}
```