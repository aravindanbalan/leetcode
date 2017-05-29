Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

For example, given the following matrix:

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
Return 6.

```java
public class Solution {
    public int maximalRectangle(char[][] matrix) {
        //Idea is to use largest rectangle area in a histogram
        //For each row find the largest rectangle area
        //for next iteration, add heights +1 if heights of next row is 1 otherwise set to zero and find the result
        
        if(matrix.length == 0 || matrix[0].length == 0) return 0;
        int m = matrix.length;
        int n = matrix[0].length;
        int[] heights = new int[n];
        
        //create initial height array
        for(int i = 0; i< heights.length ; i++){
            if(matrix[0][i] == '1')
                heights[i] = 1;
        }
        
        int result = largestRectangleSumHistogram(heights);
        
        //for each row
        for(int i = 1; i< m;i++){
            heights = preProcessHeights(heights, matrix, n, i);
            //caluclate the new rectangle area based on new heights and find max
            result = Math.max(result, largestRectangleSumHistogram(heights));
        }
        
        return result;
    }
    
    private int[] preProcessHeights(int[] heights, char[][] matrix, int n, int idx){
        for(int i = 0; i< n ;i++){
            if(matrix[idx][i] == '1') heights[i] += 1;
            else heights[i] = 0;  //reset height as no longer a valid histogram height
        }
        return heights;
    }
    
    private int largestRectangleSumHistogram(int[] heights){
        if(heights.length == 0) return 0;
        if(heights.length == 1) return heights[0];
        
        int max = 0;
        int i = 0;
        Stack<Integer> stack = new Stack<Integer>();
        
        while(i < heights.length){
            //if heights are in increasing order then push or if stack empty
            if(stack.isEmpty() || heights[stack.peek()] <= heights[i]){
                //then push
                stack.push(i++);
            }else{
                int top = stack.pop();
                int area = heights[top] * (stack.isEmpty() ? i : i- stack.peek() -1);
                max = Math.max(max, area);
                //do not increment i
            }
        }
        
        //say heights was [1,2,3,4] , then in previous step we only put everything into stack 
        while(!stack.isEmpty()){
            int top = stack.pop();
            int area = heights[top] * (stack.isEmpty() ? i : i- stack.peek() -1);
            max = Math.max(max, area);
        }
        
        return max;
    }
}
```
