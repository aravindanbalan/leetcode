Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.


Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].

```java

public class Solution {
    public int largestRectangleArea(int[] heights) {
        if(heights.length == 0) return 0;
        if(heights.length == 1) return heights[0];
        
        int maxArea = 0;
        int i = 0;
        Stack<Integer> stack = new Stack<Integer>();
        
        while(i < heights.length){
            
            if(stack.isEmpty() || heights[stack.peek()] <= heights[i]){
                stack.push(i++);
            }else{
                int top = stack.pop();
                int area = heights[top] * (stack.isEmpty() ? i : (i - stack.peek() - 1));
                
                if(maxArea < area)
                    maxArea = area;
            }
        }
        
        while(!stack.isEmpty()){
            int top = stack.pop();
            int area = heights[top] * (stack.isEmpty() ? i : (i - stack.peek() - 1));
             if(maxArea < area)
                    maxArea = area;
        }
        
        return maxArea;
    }
}
```
