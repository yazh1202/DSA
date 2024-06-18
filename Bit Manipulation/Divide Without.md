Weird solution having lots of edge cases
```java
class Solution {
    public int divide(int dividend, int divisor) {
                if (dividend == Integer.MIN_VALUE && divisor == -1) return Integer.MAX_VALUE; //Corner case when -2^31 is divided by -1 will give 2^31 which doesnt exist so overflow 
        long a = dividend;
        long b = divisor;

        if(a<0) a*=-1L;
        if(b<0) b*=-1L;
        
        boolean is = false;
        // This XOR ^ makes sure that the flag is true only if one of the conditions is satisfied and not both of them.
        is = ((dividend<0)^(divisor<0))?true:false;
        
        long ans = 0;
        System.out.println(a);
        for(long i = 31;i>=0;i--){
            if(a>=(b<<i)){
                ans += 1L<<i;
                a-=b<<i;
            }
        }
   
        if(is) ans*=-1L;
        
        return (int)ans;
    }
}
```