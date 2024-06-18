**For subsets we can go back and choose from the previous elements but cannot do it for subarrays**
[40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)


Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

**Example 1:**

**Input:** candidates = [10,1,2,7,6,1,5], target = 8
**Output:** 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]

**Example 2:**

**Input:** candidates = [2,5,2,1,2], target = 5
**Output:** 
[
[1,2,2],
[5]
]

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> ans =  new ArrayList<>();

        Arrays.sort(candidates);
        recur(0,0,ans,new ArrayList<>(),target,candidates);
        return ans;
    }
    static void recur(int pos,int cs,List<List<Integer>> ans,ArrayList<Integer> curr,int tgt,int[] nums){

        if(cs==tgt) {
            ans.add(new ArrayList<Integer>(curr));
            return;
        }
        // Removing this will create lots of 
        // unwanted recursive calls
        if(cs>tgt||pos>=nums.length) return;
        for(int i = pos;i<nums.length;i++){
            if(i>pos&&nums[i]==nums[i-1]) continue;

            if(nums[i]>tgt) break;
            curr.add(nums[i]);
            recur(i+1,cs+nums[i],ans,curr,tgt,nums);
            curr.remove(curr.size()-1);
        }
    }
}

```