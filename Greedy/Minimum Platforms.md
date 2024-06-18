### Minimum Platforms

Given arrival and departure times of all trains that reach a railway station. Find the minimum number of platforms required for the railway station so that no train is kept waiting.  

Consider that all the trains arrive on the same day and leave on the same day. Arrival and departure time can never be the same for a train but we can have arrival time of one train equal to departure time of the other. At any given instance of time, same platform can not be used for both departure of a train and arrival of another train. In such cases, we need different platforms.


[TLINK](https://takeuforward.org/data-structure/minimum-number-of-platforms-required-for-a-railway/)


```python
class Solution:    
	# The key is to find overlaps
	# If the next greater timing is a departure we
	# increment else if it is the arrival timing we decrement
    def minimumPlatform(self,n,arr,dep):
        
        arr.sort()
        dep.sort()
        
        i,j = 0,0
        ans,curr = 0,0
        
        while i<n:
            
            if arr[i]<=dep[j]:
                curr+=1
                ans = max(curr,ans)
                i+=1
            else:
                curr-=1
                j+=1
                
            
        return ans
```