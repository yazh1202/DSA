
[Problem Link](https://www.codingninjas.com/studio/problems/day-23-:-infix-to-postfix-_1382146)
	
```java
import java.util.*;

public class Solution {
    public static String prefixToInfixConversion(String exp) {
		// Doing it reverse for easineess
        StringBuilder sb =  new StringBuilder(exp);
        sb.reverse();
        StringBuilder ans =  new StringBuilder(exp);
		
        Stack<String> st = new Stack<>();
		
        for(char c:sb.toString().toCharArray()){
			
            if(Character.isLetterOrDigit(c)){
                st.push(String.valueOf(c));
            }else{
            // If operand then performing the operation and storing expression onto the stack
                StringBuilder temp = new StringBuilder();
                temp.append(st.pop());
                temp.append(c);
                temp.append(st.pop());
                st.push("("+temp.toString()+")");        
            }
        }
        return st.peek();
    }
}
```