
**Problem Statement:*** Given an integer array arr of size N, sorted in ascending order (with distinct values) and a target value k. Now the array is rotated at some pivot point unknown to you. Find the index at which k is present and if k is not present return -1.-

**Intuition =  One part will always be sorted..**

```java
class Solution {
    public int search(int[] nums, int target) {
        
            int n = nums.length;

            int i = 0, j=n-1;

            while(i<=j){
                int mid = i+(j-i)/2;

                if(nums[mid]==target) return mid;

                // Sorted From mid to start
                if(nums[mid]>=nums[i]){
                    if(nums[mid]>=target&&target>=nums[i]){
                        j = mid-1;
                    }else{
                        i = mid+1;
                    }
                }
                else {
                    if(nums[mid]<=target&&nums[j]>=target){
                        i = mid+1;
                    }else{
                        j = mid-1;
                    }
                }
            }
        return -1;
    }
}
```