```java
        // Getting the bit value at
        int temp = num;// num is input value
        ans[0] = (temp&(1<<i))>0?1:0;
        
        // Setting the i bit
        temp = temp | (1<<i);
        ans[1] = temp;

        // Clearing the i bit
        temp = num;// Since we changed temp last time.
        temp = temp & ~(1<<i);
        ans[2] = temp;

        return ans;
```

# XOR ( eXclusive OR )
![[Pasted image 20240112100651.png]]
[Swapping Problem](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)]
[More Info](https://accu.org/journals/overload/20/109/lewin_1915/)

```java
public class Solution{
    public static void swapNumber(int []a, int []b) {
        int temp = a[0]^b[0];
        a[0] = a[0]^temp;
        b[0] = temp^b[0];    
    }
}
```

## Single Number
Given a **non-empty** array of integers `nums`, every element appears _twice_ except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.


```java
class Solution {
    public int singleNumber(int[] nums) {
        // Because xor with a number itself will result in 
        // 0 and then xor with the single number will 
        // result in the number itself.
        int ans = 0;
        for(int i = 0;i<nums.length;i++){
            ans =  ans ^ nums[i];
        }
        return ans;
    }
}
```
