
## If unique then
[Problem Link](https://leetcode.com/problems/search-in-rotated-sorted-array/)
```java
class Solution {
    public boolean search(int[] nums, int target) {
        
        int n = nums.length;
        int i = 0,j = n-1;

        while(j>=i){

            int mid = i + (j-i)/2;
            if(nums[mid]==target) return true;

				// If the left half is sorted
            if(nums[mid]>=nums[i]){
	              // target in left half
                if(target<nums[mid]&&target>=nums[i]){
                    j = mid-1;
                }else{
	                // remove this half if not 
                    i = mid+1;
                }
                // if the right half is sorted
            }else{
		        // if target in right half
                if(target>nums[mid]&&target<=nums[j]){
                    i = mid+1;
                }else{
                // remove this half if not 
                    j = mid-1;
                }
            }
        }
        return false;
    }
}
```

## If not unique
[Problem Link](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

```java
// Only this condition will fail as it won't be able 
// to tell which half is sorted
// as in 1 0 1 1 1. So handle this case by reducing both.
if(nums[mid]==nums[i]&&nums[l]==nums[h]){
                i++;
                j--;
                continue;
}
```


## Number of rotations
[Problem Link](https://www.codingninjas.com/studio/problems/rotation_7449070?leftPanelTabValue=PROBLEM)

```java
public class Solution {
    public static int findKRotation(int []arr){
      int n = arr.length;
      int low = 0,high=n-1;
      int ans = Integer.MAX_VALUE;
      int ind = 0;
      while(high>=low){
          int mid = low + (high-low)/2;
			// If both the ends are sorted then return low
            if (arr[low] <= arr[high]) {
                if (arr[low] < ans) {
                    ind = low;
                    ans = arr[low];
                }
                break;
            }
          if(arr[mid]>=arr[low]){
              if(ans>arr[low]){
                  ans = arr[low];
                  ind = low;
                  
              }
              low = mid+1;
          }else{
                if(ans>arr[mid]){
                  ans = arr[mid];
                  ind = mid;
                }        
              high = mid-1;
          }
      }
      return ind;
    }
}
```