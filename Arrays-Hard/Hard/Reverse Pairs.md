
[493. Reverse Pairs](https://leetcode.com/problems/reverse-pairs/)

Given an integer array `nums`, return _the number of **reverse pairs** in the array_.

A **reverse pair** is a pair `(i, j)` where:

- `0 <= i < j < nums.length` and
- `nums[i] > 2 * nums[j]`.

**Example 1:**

**Input:** nums = [1,3,2,3,1]
**Output:** 2
**Explanation:** The reverse pairs are:
(1, 4) --> nums[1] = 3, nums[4] = 1, 3 > 2 * 1
(3, 4) --> nums[3] = 3, nums[4] = 1, 3 > 2 * 1

**Example 2:**

**Input:** nums = [2,4,3,5,1]
**Output:** 3
**Explanation:** The reverse pairs are:
(1, 4) --> nums[1] = 4, nums[4] = 1, 4 > 2 * 1
(2, 4) --> nums[2] = 3, nums[4] = 1, 3 > 2 * 1
(3, 4) --> nums[3] = 5, nums[4] = 1, 5 > 2 * 1

**Constraints:**

- `1 <= nums.length <= 5 * 104`
- `-231 <= nums[i] <= 231 - 1`

>[!Intuition]
>The optimal solution would be a slight modification of merge sort and [[Count Inversions]] condition where we find the possible reverse pairs when we have already sorted two parts of the array.




```python
class Solution:
    def reversePairs(self, nums: List[int]) -> int:
        ans = self.sort([0],0,len(nums)-1,nums)
        print(nums)
        return ans[0]
    
    def sort(self,count,low,high,arr):
        if high>low:
            mid = (high+low)//2
            self.sort(count,low,mid,arr)
            self.sort(count,mid+1,high,arr)
            count[0]+=self.merge(arr,low,mid,high)
        return count

    # The modification required which just finds the possible pairs
    # Using two sorted arrays
    def countPairs(self,arr, low, mid, high):
        right = mid + 1
        cnt = 0
        for i in range(low, mid + 1):
            while right <= high and arr[i] > 2 * arr[right]:
                right += 1
            cnt += (right - (mid + 1))
        return cnt

    def merge(self,arr,low,mid,high):
        i,j,k = low,mid+1,0
        store = [0]*(high-low+1)
        count = self.countPairs(arr,low,mid,high)
        while i<=mid and j<=high:
            if arr[i]<arr[j]:
                store[k] = arr[i]
                i,k = i+1,k+1
            else:                
                store[k] = arr[j]
                j,k = j+1,k+1
        
        while i<=mid:
            store[k] = arr[i]
            i,k = i+1,k+1
        
        while j<=high:
            store[k] = arr[j]
            j,k = j+1,k+1
        k = 0
        for i in range(low,high+1):
            arr[i] = store[k]
            k+=1
        return count
```

>[!Compelxities]
**Time Complexity:** O(2N*logN), where N = size of the given array.  
**Reason:** Inside the mergeSort() we call merge() and countPairs() except mergeSort() itself. Now, inside the function countPairs(), though we are running a nested loop, we are actually iterating the left half once and the right half once in total. That is why, the time complexity is O(N). And the merge() function also takes O(N). The mergeSort() takes O(logN) time complexity. Therefore, the overall time complexity will be O(logN * (N+N)) = O(2N*logN).
   **Space Complexity:** O(N), as in the merge sort We use a temporary array to store elements 
   in sorted order.
   

