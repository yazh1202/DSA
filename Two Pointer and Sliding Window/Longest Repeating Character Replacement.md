
>[!Intuition]
>The main intuition is that the window will always have a most frequent character and other characters will need to be converted into it for optimal results
> The sliding window will move and remove the characters no longer part of the window.


>
```java
class Solution {
    public int characterReplacement(String s, int k) {
        
        HashMap<Character,Integer> hm = new HashMap<>();
        int n = s.length();
        int i =0,j=0;
        int res = 0;
        while(j<n){
            char c = s.charAt(j);
            hm.put(c,hm.getOrDefault(c,0)+1);

            while(j-i+1-max(new ArrayList<Integer>(hm.values()))>k){
                char temp = s.charAt(i);
                hm.put(temp,hm.get(temp)-1);
                i++;
            }
            res = Math.max(j-i+1,res);
            j++;
        }

        return res;
    }

    static int max(ArrayList<Integer> arl){
        int ans = -1;
        for(int i:arl){
            ans = Math.max(ans,i);
        }
        return ans;
    }
}
```