
[930. Binary Subarrays With Sum](https://leetcode.com/problems/binary-subarrays-with-sum/)

Given a binary array `nums` and an integer `goal`, return _the number of non-empty **subarrays** with a sum_ `goal`.

A **subarray** is a contiguous part of the array.

**Example 1:**

**Input:** nums = [1,0,1,0,1], goal = 2
**Output:** 4

**Input:** nums = [0,0,0,0,0], goal = 0
**Output:** 15

>[!First Method]
>The first method involves using the same principle as the subarrays with sum k problem which uses hashmap to store sum of elements at each interval and then checks if the current element has a match for **current_sum-k** in the hashmap and if it does it means that there is a subarray that will add up to k between current element and previous element.


```java
class Solution {
    public int numSubarraysWithSum(int[] nums, int k) {
        int n = nums.length;
        int ans = 0;
        HashMap<Integer,Integer> hm = new HashMap<>();
        hm.put(0,1);
        int sum = 0;
        for(int i:nums){
            sum+=i;
            // This is the matching process
            if(hm.containsKey(sum-k)){
	            // This take care of the possible negatives or zeroes in subarrays with sum k problem but here only takes care of zeroes in the subarrays which will lead to same sum in multiple arrays
                ans+=hm.get(sum-k);
            }
            hm.put(sum,hm.getOrDefault(sum,0)+1);
        }
        return ans;
    }
}
```


>[!Method 2]
>Don't really understand how this method works leaving it here for now
>The idea comes from probability that the difference between all the subarrays having atmost sum k and subarrays having sum atmost k-1 will be the number of the subarrays having sum k.
>And the sliding window application allows to find the number of subarrays having sum upto k not the number of subarrays having sum k.




```java
class Solution {
    public int numSubarraysWithSum(int[] nums, int k) {
        return atmostK(nums,k)-atmostK(nums,k-1);
    }

    static int atmostK(int[] nums,int k){

        int st = 0,en=0,ans=0,sum=0;

        int n = nums.length;
        for(en = 0;en<n;en++){
            sum+=nums[en];
            while(sum>k&&st<=en){
                sum-=nums[st];
                st++;
            }
            ans+=(en-st+1);
        }
        return ans;
    }
}
```

Similar Problem - 
[1248. Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/)

Given an array of integers `nums` and an integer `k`. A continuous subarray is called **nice** if there are `k` odd numbers on it.

Return _the number of **nice** sub-arrays_.

```java
class Solution {
    public int numberOfSubarrays(int[] nums, int k) {
        return atMostK(nums,k)-atMostK(nums,k-1);
    }

    static int atMostK(int[] nums,int k){
    // The only change is that now we count the odd elements 
    // rather that ones or zeroes
        int cnt = 0;
        int sum = 0;
        int i = 0,j=0;
        int n = nums.length;
        while(j<n){
            if(nums[j]%2!=0) sum++;
            while(i<n&&sum>k) {
                if(nums[i]%2!=0) sum--;
                i++;
            }
            cnt+=(j-i+1);
            j++;
        }
        return cnt;
    }
}
```