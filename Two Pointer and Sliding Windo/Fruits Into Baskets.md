```java
class Solution {
    public int totalFruit(int[] fruits) {
        int n = fruits.length;

        int fb = 0;
        int sb = 0;
        int sbc = 0;

        int cm = 0;
        int ans = 0;

        for(int i:fruits){
            
            if(i==fb||i==sb) {
                cm++;
            }else {
                cm = sbc+1;
            }
            
            if(i==sb){
                sbc++;
            }else{
                sbc=1;
            }
            if(i!=sb){
                fb = sb;
                sb = i;
            }

            ans = Math.max(cm,ans);
        }

        return ans;
    }
}
```