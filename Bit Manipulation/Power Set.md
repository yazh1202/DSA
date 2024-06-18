
Given an integer array `nums` of **unique** elements, return _all possible_ 

_subsets_

 _(the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        
        // Using Bit Manipulation
        int n = nums.length;
        int end = (1<<n)-1;
        List<List<Integer>> ls = new ArrayList<>();

        // 0 to 2^n-1 covers all possible subsets of 
        // the set
        for(int i = 0;i<=end;i++){
            ArrayList<Integer> temp = new ArrayList<>();
            for(int j = 0;j<n;j++){
                // This 'if' will tell us if the bit at jth position is set or not
                // If it is set then we add the number to the temporary arraylist
                if((i & (1<<j))>=1){
                    temp.add(nums[j]);
                }
            }
            ls.add(new ArrayList<Integer>(temp));
        }
        return ls;
    }
}
```

>If we **bitwise AND** a number with its negative counterpart, we get rightmost set bit.
>