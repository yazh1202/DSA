

```java
import java.util.Stack;

public class Solution {
    
	public static void reverseStack(Stack<Integer> stack) {
		if(stack.isEmpty()) return;
		int data = stack.pop();
		
		reverseStack(stack);
		mkem(stack,data);
	}

	static void mkem(Stack<Integer> st, int data){
		if(st.isEmpty()) {
			st.push(data);
			return;
		}
		int val = st.pop();
		mkem(st,data);
		st.push(val);
	}
}
```