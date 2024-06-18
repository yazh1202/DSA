[Kth Missing Number](https://takeuforward.org/arrays/kth-missing-positive-number/)

```java
class Solution {
    public int findKthPositive(int[] arr, int k) {
        int n = arr.length;
        int low = 0,high = n-1;
        int count = arr[low]-1;
        while(high>=low){
            int mid = (low+high)/2;

            count=arr[mid]-(mid+1);
            if(count<k){
                low = mid+1;
            }else{
                high = mid-1;
            }
        }
        /**- _more_missing_numbers = k - (vec[high] - (high+1))_.
        Now, we will simply add more_missing_numbers to the
        preceding neighbor i.e. vec[high] to get the kth missing
        number.  
        kth missing number = vec[high] + k - (vec[high] - (high+1)) 
            =  vec[high] + k - vec[high] + high + 1  
            = k + high + 1. 
        **/
        return k+high+1;

    }
}
```