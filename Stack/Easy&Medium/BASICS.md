# Implementing QUEUE using Two Stacks
```java
class MyQueue {
    Stack<Integer> st = new Stack<>();
    Stack<Integer> en = new Stack<>();
    public MyQueue() {
        
    }
    
    public void push(int x) {
        // O(1)
        st.push(x);
    }
    
    public int pop() {
        // Transferring to the second stack
        while(!st.isEmpty()){
            en.push(st.pop());
        }
        // Popping from the second stack which is in 
        // reverse order now
        int a = en.pop();
        return a;
    }
    
    public int peek() {
        // If the stacks have not been reversed
        // Reverse it
        if(en.isEmpty()){
            while(!st.isEmpty()){
                en.push(st.pop());
            }
        }
        // Returns top of reversed stack
        return en.peek();
    }
    
    public boolean empty() {
        return st.isEmpty() && en.isEmpty();
    }
}

```

## Other types
[Stack with linked List](https://www.codingninjas.com/studio/problems/implement-stack-with-linked-list_1279905?leftPanelTabValue=SUBMISSION)
[Queue With Linked List](https://www.codingninjas.com/studio/problems/implement-queue-using-linked-list_8161235?leftPanelTabValue=SUBMISSION)
