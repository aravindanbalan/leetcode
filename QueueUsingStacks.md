Implement the following operations of a queue using stacks.

push(x) -- Push element x to the back of queue.
pop() -- Removes the element from in front of queue.
peek() -- Get the front element.
empty() -- Return whether the queue is empty.
Notes:
You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

```java
public class MyQueue {

    Stack<Integer> newestOnTop;
    Stack<Integer> oldestOnTop;
    /** Initialize your data structure here. */
    public MyQueue() {
        newestOnTop = new Stack<Integer>();
        oldestOnTop = new Stack<Integer>();
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        //always we push into the newstonTop stack
        newestOnTop.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        //always remove from oldestOnTop
        shuffleStacks();
        return oldestOnTop.pop();
    }
    
    /** Get the front element. */
    public int peek() {
        shuffleStacks();
        return oldestOnTop.peek();
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return newestOnTop.isEmpty() && oldestOnTop.isEmpty();
    }
    
    private void shuffleStacks(){
        if(oldestOnTop.isEmpty()){
            while(!newestOnTop.isEmpty()){
                oldestOnTop.push(newestOnTop.pop());
            }
        }
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```
