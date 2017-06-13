```
Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

For example, given the following matrix:

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
Return 4.

```

```java
public class Solution {
    public int maximalSquare(char[][] matrix) {
        //We can use dp to solve this problem
        
        //The idea is that if there is a 1 in the original matrix, check the top, left and top left elements to see whats the minimum number of 1s it had, if there was a zero , then take the minimum so that we have only ones in the end matrix
        
        if(matrix.length == 0 || matrix[0].length == 0) return 0;
        int m = matrix.length; 
        int n = matrix[0].length;
        
        int[][] dp = new int[m+1][n+1];
        int result = 0;
        
        //O(mn)
        for(int i = 1; i<=m ; i++){
            for(int j = 1; j<=n ; j++){
                if(matrix[i-1][j-1] == '1'){
                    dp[i][j] = Math.min(Math.min(dp[i-1][j], dp[i][j-1]), dp[i-1][j-1]) + 1;
                    result = Math.max(result, dp[i][j]);
                }
            }
        }
        
        return result*result;
    }
}
```
