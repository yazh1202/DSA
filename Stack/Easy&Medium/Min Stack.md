Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

```java
class MinStack {
// Need to use long for everything as integer over/underflow problems are encountered otherwise
    Stack<Long> st = new Stack<Long>();
    Long min = Long.MAX_VALUE;

    public MinStack() {
        
    }
    
    public void push(int val) {
        Long value = Long.valueOf(val);

        if(st.isEmpty()){
            min = value;
            st.push(value);
        }else if(min>value){
        // Storing modified value which can used to obtain min before that index
        // 2*value-min will always be lesser than value
            st.push(2*value-min);
            min = value;
        } else{
            st.push(value);
        }
    }
    
    public void pop() {
        Long val = st.pop();
        if(val<min){
        //  Checking if minima was there
            min = 2*min-val; 
        }
    }
    
    public int top() {
        Long val = st.peek();
        if(val<min){
            return min.intValue();
        }
        return val.intValue();
    }
    
    public int getMin() {
        return min.intValue();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```