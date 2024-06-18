Problem statement
You are given an array 'arr' of size 'n'.



It contains an even number of occurrences for all numbers except two numbers.



Find those two numbers which have odd occurrences and return in decreasing order.



Example:
For 'arr' = {2, 4, 1, 3, 2, 4} , 'n' = 6.
Answer is {3, 1}.
Here, numbers 1, 3 have occurrence 1 i.e. odd and numbers 2, 4 have occurrence 2 i.e. even.
**Relates to properties of XOR and & operation of x and -x**

[Explanation Link](https://www.geeksforgeeks.org/find-the-two-numbers-with-odd-occurences-in-an-unsorted-array/)

```java
public class Solution {
    public static int[] twoOddNum(int []arr){
        int xor = 0;
        int n = arr.length;
        // Finding XOR of all
        for(int i:arr){
            xor = xor ^ i;
        }

        // Finding set bit number, the numbers will have different values 
        // at this bit
        int setbit = (xor & -xor); 
        
        // The x and y will store the XOR's of the 
        // numbers and will eventually become the answers
        // due to the XOR's identity property of a^a = 0
        // and 0^a = a
        int x = 0;
        int y = 0;

        for(int i:arr){

            if((i&setbit)>0) {
                x = x ^ i;
            }else{
                y = y^i;
            }
        }

        int[] ans = new int[2];
        ans[1] = Math.min(x,y);
        ans[0] = Math.max(x,y);
        return ans;

    }
}
```