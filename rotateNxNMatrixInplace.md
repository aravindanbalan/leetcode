You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Follow up:
Could you do this in-place?

```java

public class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        if(n == 0 || n ==1){
            return;
        }
        
        //In place rotation can be done only when its a square matrix
        
        //we need a loop which goes level by level till the inner most value
        for(int level = 0; level < n/2 ; level++){
            int first = level;
            int last = n - level -1; // -1 is for index starting at 0
            
            //we need a loop which goes thru each element in the row
            for(int i = first; i < last ; i++){
                int offset = i - first; // denotes the offset from the start if you are in the middle of the row
                
                //save top
                int top = matrix[first][i];
                
                //left -> top
                matrix[first][i] = matrix[last - offset][first];
                
                //bottom -> left
                matrix[last - offset][first] = matrix[last][last-offset];
                
                //right-> bottom
                matrix[last][last-offset] = matrix[i][last];
                
                //top->right
                matrix[i][last] = top;
            }
        }
    }
}
```
