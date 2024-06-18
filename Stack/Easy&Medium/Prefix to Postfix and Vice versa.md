
```java

import java.util.*;

public class Solution {
    public static String preToPost(String exp) {
        
        StringBuilder sb =  new StringBuilder(exp);
        sb.reverse();

        Stack<String> st = new Stack<>();

        for(char c:sb.toString().toCharArray()){

            if(Character.isLetterOrDigit(c)){
                st.push(String.valueOf(c));
            }else{
                StringBuilder temp = new StringBuilder();
                
                temp.append(st.pop());
                temp.append(st.pop());
                temp.append(c);
                st.push(temp.toString());        
            }
        }
        return st.peek();
    }
}
```

## Postfix to Prefix

>[!IMPORTANT]
>  Need to put the second operand in stack as first in expression due to the right to left nature of prefix .Everything else remains same


```

```java
import java.util.*;
public class Solution {
    public static String postfixToPrefix(String exp) {
       
        StringBuilder sb =  new StringBuilder(exp);

        Stack<String> st = new Stack<>();

        for(char c:sb.toString().toCharArray()){

            if(Character.isLetterOrDigit(c)){
                st.push(String.valueOf(c));
            }else{
                StringBuilder temp = new StringBuilder();
                temp.append(c);
                // Need to put the second in stack as first operand 
                // due to the right to left nature of prefix
                // Everything else remains same
                String a = st.pop();
                String b = st.pop();
                temp.append(b);
                temp.append(a);
                
                st.push(temp.toString());        
            }
        }
        return st.peek();
    }
}
```