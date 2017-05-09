```
Given a 2D matrix matrix, find the sum of the elements inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).

Range Sum Query 2D
The above rectangle (with the red border) is defined by (row1, col1) = (2, 1) and (row2, col2) = (4, 3), which contains sum = 8.

Example:
Given matrix = [
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]

sumRegion(2, 1, 4, 3) -> 8
sumRegion(1, 1, 2, 2) -> 11
sumRegion(1, 2, 2, 4) -> 12

Note:
You may assume that the matrix does not change.
There are many calls to sumRegion function.
You may assume that row1 ≤ row2 and col1 ≤ col2.
```

```java
public class NumMatrix {

    int[][] sum;
    public NumMatrix(int[][] matrix) {
        if(matrix == null || matrix.length == 0 || matrix[0].length == 0){
            return;   
        }
        int m = matrix.length;
        int n = matrix[0].length;
        
        sum = new int[m+1][n+1];
        
        for(int i = 1; i <= m;i++){
            for(int j = 1 ;j<=n ;j++){
                sum[i][j] = sum[i-1][j] + sum[i][j-1] - sum[i-1][j-1] + matrix[i-1][j-1];
            }
        }
    }
    
    public int sumRegion(int row1, int col1, int row2, int col2) {
        int iMin = Math.min(row1, row2) +1;
        int iMax = Math.max(row1, row2) +1;
        int jMin = Math.min(col1, col2) +1;
        int jMax = Math.max(col1, col2) +1;
        
        //sum equals bottom right corner sum - top right corner sum - bottom left corner sum + common top left corner sum (as it was added twice)
        return sum[iMax][jMax] - sum[iMin -1][jMax] - sum[iMax][jMin-1] + sum[iMin-1][jMin-1];
    }
}

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix obj = new NumMatrix(matrix);
 * int param_1 = obj.sumRegion(row1,col1,row2,col2);
 */
```
