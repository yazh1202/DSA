>[!Intuition]
>The intuition is from the brute-force where we check for the left max and right max for each index, here we just use two pointers to make sure that the answer is added in both cases of the left or right part being minimum.
>


```java
class Solution {
    public int trap(int[] ht) {
        // Optimal
        int n = ht.length;
        int i =0,j=n-1;
        int lm = -1,rm=-1;
        
        int ans = 0;

        while(i<j){
            if(ht[i]<=ht[j]){
                if(lm<=ht[i]) lm = ht[i];
                else ans+=(lm-ht[i]);
                i++;
            }else{
                if(rm<=ht[j]) rm = ht[j];
                else ans+=(rm-ht[j]);
                j--;
            }
        }
        return ans;

    }
}

```