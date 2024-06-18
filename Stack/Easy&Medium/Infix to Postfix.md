[Problem Link](https://www.codingninjas.com/studio/problems/day-23-:-infix-to-postfix-_1382146?leftPanelTabValue=SUBMISSION)
[Video Explaination](https://www.youtube.com/watch?v=m7SGekhd1mQ)
```java


import java.util.*;

public class Solution {
    public static String infixToPostfix(String exp) {
        Stack<Character> st = new Stack<>();
        StringBuilder sb = new StringBuilder();
        for(char c:exp.toCharArray()){
            // If Opening bracket is found simply push it onto the stack

            if(c=='('){
                st.push(c);
            }else if(c==')'){
            // If ')' add the operands to the expression till '(' found
                while(!st.isEmpty()&&st.peek()!='('){
                    char ch = st.pop();
                    sb.append(ch);
                }
                // Remove the '('
                st.pop();
            }else if(Character.isLetterOrDigit(c)){
                sb.append(c);
            }else{
                while(!st.isEmpty()&&prec(st.peek())>=prec(c)){
                        sb.append(st.pop());
                    }
                st.push(c);
            }
        }
        while(!st.isEmpty()) sb.append(st.pop());

        return sb.toString();
    }
    static int prec(char ch) {
        switch (ch) {
        case '+':
        case '-':
        return 1;

        case '*':
        case '/':
        return 2;

        case '^':
        return 3;
        }
        return -1;
  }
}
```