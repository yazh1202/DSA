
[1358. Number of Substrings Containing All Three Characters](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/)

Given a string `s` consisting only of characters _a_, _b_ and _c_.

Return the number of substrings containing **at least** one occurrence of all these characters _a_, _b_ and _c_.

```java
class Solution {
    public int numberOfSubstrings(String s) {
        int a = 0,b=0,c=0;
        int n = s.length();
        int ans = 0;
        int[] store = new int[3];
        int i=0,j=0;
        while(j<n){
            char ch = s.charAt(j);
            store[(int)(ch-'a')]++;
            // We can be sure that the current window subarray will
            // make a subarray with the rest of the elements as it              // already has satisfied the conditions 
            while(i<n&&store[0]>=1&&store[1]>=1&&store[2]>=1){
                ans+=n-j;
                store[s.charAt(i)-'a']--;
                i++;
            }
            j++;
        }
        return ans;
    }
}
```