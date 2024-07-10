
[1423. Maximum Points You Can Obtain from Cards](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/)

There are several cards **arranged in a row**, and each card has an associated number of points. The points are given in the integer array `cardPoints`.

In one step, you can take one card from the beginning or from the end of the row. You have to take exactly `k` cards.

Your score is the sum of the points of the cards you have taken.

Given the integer array `cardPoints` and the integer `k`, return the _maximum score_ you can obtain.

**Input:** cardPoints = [1,2,3,4,5,6,1], k = 3
**Output:** 12
**Explanation:** After the first step, your score will always be 1. However, choosing the rightmost card first will maximize your total score. The optimal strategy is to take the three cards on the right, giving a final score of 1 + 6 + 5 = 12.

>[!Intuition] 
>The main intuition is the mix and match of the k sized arrays from first and last arrays


```java
class Solution {
    public int maxScore(int[] CP, int k) {
        int n = CP.length;
        int ans = 0;
        int sum = 0;
        for(int i = 0;i<k;i++){
            sum+=CP[i];
        }
        int i = k-1;
        // Takign some part of last ends and removing first ends 
        ans = sum;
        for(int j = n-1;j>=n-k;j--){
            sum-=CP[i--];
            sum+=CP[j];
            ans = Math.max(ans,sum);
        }
        return ans;
        
    }
}
```