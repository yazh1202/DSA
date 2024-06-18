Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer (similar to C/C++'s `atoi` function).

The algorithm for `myAtoi(string s)` is as follows:

1. Read in and ignore any leading whitespace.
2. Check if the next character (if not already at the end of the string) is `'-'` or `'+'`. Read this character in if it is either. This determines if the final result is negative or positive respectively. Assume the result is positive if neither is present.
3. Read in next the characters until the next non-digit character or the end of the input is reached. The rest of the string is ignored.
4. Convert these digits into an integer (i.e. `"123" -> 123`, `"0032" -> 32`). If no digits were read, then the integer is `0`. Change the sign as necessary (from step 2).
5. If the integer is out of the 32-bit signed integer range `[-231, 231 - 1]`, then clamp the integer so that it remains in the range. Specifically, integers less than `-231` should be clamped to `-231`, and integers greater than `231 - 1` should be clamped to `231 - 1`.
6. Return the integer as the final result.

**Note:**

- Only the space character `' '` is considered a whitespace character.
- **Do not ignore** any characters other than the leading whitespace or the rest of the string after the digits.

**Example 1:**

**Input:** s = "42"
**Output:** 42
**Explanation:** The underlined characters are what is read in, the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "42" ("42" is read in)
           ^
The parsed integer is 42.
Since 42 is in the range [-231, 231 - 1], the final result is 42.

```java
class Solution {
    public int myAtoi(String s) {
          int n = s.length();
        int i = 0;
        int sign = 1;
        // Skipping whitespaces
        while(i<n && s.charAt(i)==' ') {
            i++;
        }
        //If empty return 0
        if (i>=n) {
            return 0;
        }
        // If first character is negative then mark negative
        if (s.charAt(i)=='-') {
            sign = -1;
        }
        // Else move on 
        if (s.charAt(i)=='+' || s.charAt(i)=='-') {
            i++;
        }
        // Again if end return 0
        if (i>=n) {
            return 0;
        }
        int num = 0;
        while (i<n && s.charAt(i)>='0' && s.charAt(i)<='9') {
            int x = s.charAt(i)-'0';
            // If current number is grateer than
            // Integer.MAX_VALUE/10
            // then return max or min depending upon sign
            if (num>Integer.MAX_VALUE/10 || (num==Integer.MAX_VALUE/10 && x>Integer.MAX_VALUE%10)) {
                if (sign==1) {
                    return Integer.MAX_VALUE;
                }
                else {
                    return Integer.MIN_VALUE;
                }
            }
            num = num*10 + x;
            i++;
        }
        return num*sign; 
    }
}
```