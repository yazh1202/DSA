
>[!Intuition] Main intuition is that each call to know will always eliminate one of the candidate for being the celebrity
## Problem statement

There are ‘N’ people at a party. Each person has been assigned a unique id between 0 to 'N' - 1(both inclusive). A celebrity is a person who is known to everyone but does not know anyone at the party.

Given a helper function ‘knows(A, B)’, It will returns "true" if the person having id ‘A’ know the person having id ‘B’ in the party, "false" otherwise. Your task is to find out the celebrity at the party. Print the id of the celebrity, if there is no celebrity at the party then print -1.

**Note:**

```
1. The helper function ‘knows’ is already implemented for you.
2. ‘knows(A, B)’ returns "false", if A doesn't know B.
3. You should not implement helper function ‘knows’, or speculate about its implementation.
4. You should minimize the number of calls to function ‘knows(A, B)’.
5. There are at least 2 people at the party.
6. At most one celebrity will exist.
```

```java
import java.util.* ;
import java.io.*; 
/*
	This is signature of helper function 'knows'.
	You should not implement it, or speculate about its implementation.

	boolean knows(int A, int B); 
	Function 'knows(A, B)' will returns "true" if the person having
	id 'A' know the person having id 'B' in the party, "false" otherwise.
	Use it as Runner.knows(A, B);
*/
	
public class Solution {
	public static int findCelebrity(int n) {
        //if a knows be then a will be removed and b put back into the stack
		Stack<Integer> st = new Stack<>();
		for(int i  = 0;i<n;i++){
			st.push(i);
		}
		
		while(st.size()>=2){
			int a = st.pop();
			int b = st.pop();
			// If a knows b then a cannot be celebrity
			if(Runner.knows(a,b)){
				st.push(b);
			// If a does not know b then b cannot be a celebrity
			}else{
				st.push(a);
			}
		}

		if(st.isEmpty()) return -1;

		int ch = st.peek();
		// Checking if the current candidate is known by all and does not know anyone
		for(int i = 0;i<n;i++){
			if(i==ch) continue;
			if(!Runner.knows(i,ch)||Runner.knows(ch,i)) return -1;
		}
		// SC = O(n)
		// TC = O(n)
		return ch;

    }
}
```