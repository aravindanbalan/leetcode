Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.

```java
public class MinStack {

    /** initialize your data structure here. */
    int min = Integer.MAX_VALUE;
    Stack<Integer> stack;
    
    public MinStack() {
        stack =  new Stack<>();
    }
    
    public void push(int x) {
        if(x <= min){
            stack.push(min); //push old min first;
            min = x; //reset min to current x;
        }
        stack.push(x); //now push current x;
    }
    
    public void pop() { 
        if(stack.pop() == min) //if top value is current min, then restore the previous min by popping again.
            min = stack.pop(); //restores old min value
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```
