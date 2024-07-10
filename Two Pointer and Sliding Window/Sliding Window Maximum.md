[239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

>[!Intuition]
>The main intuition is that we will need the maximum within the sliding window and if we encounter a new maximum then the previous one will no longer be needed and we can remove it.
>Also we need to remove elements out of the current window.
>




```python
from collections import deque 

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        ans = []
        # This is needed to make sure that we can pop
        # and peek at both ends to maintain order
        dq = deque()
        
        for ind,val in enumerate(nums):
            # The element at the left will be the oldest
            # and will be removed first

            if dq and dq[0]==ind-k:
                dq.popleft()
            # This makes sure that the order is maintained
            # by removing the least recent smaller element
            while dq and nums[dq[-1]]<val:
                dq.pop()
            # Appending at the end to make sure it is used later if needed
            dq.append(ind)

            if ind>=k-1:
                ans.append(nums[dq[0]])
            
        return ans


```