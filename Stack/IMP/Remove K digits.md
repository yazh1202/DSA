

>[Intuition]
>The lowest number will have the numbers in increasing order in them with the leftmost parts having higher priority.

```java
class Solution {
    public String removeKdigits(String num, int k) {

        if(k>=num.length()) return "0";
        LinkedList<Integer> st = new LinkedList<>();
        int rem = 0;
        for(char c:num.toCharArray()){
            int nm = (int)(c-'0');
            if(st.isEmpty()||nm>st.peek()){
                st.push(nm);
            }else{
                while(!st.isEmpty()&&st.peek()>nm&&rem<k){
                    st.pop();
                    rem++;
                }
                st.push(nm);
            }
        }
		// If all are increasing we will remove the last ones
		// E.g 1234 
        while(!st.isEmpty()&&rem<k) {
            st.pop();
            rem++;
        }
        
        String s = "";
        // If any of them have leading zeroes
        while(!st.isEmpty()&&st.peekLast()==0) st.removeLast();
        // If nothing remains go 0
        if(st.isEmpty()) return "0";

        while(!st.isEmpty()){
            s += String.valueOf(st.removeLast());
        }
        
        return s;
    }
}

```

