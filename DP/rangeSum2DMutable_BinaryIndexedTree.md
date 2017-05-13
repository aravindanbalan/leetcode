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
update(3, 2, 2)
sumRegion(2, 1, 4, 3) -> 10
```

```java
public class NumMatrix {

    int[][] BIT;
    int[][] nums;
    int m;
    int n;
    
    public NumMatrix(int[][] matrix) {
        if(matrix.length == 0 || matrix[0].length ==0) return;
        m = matrix.length;
        n = matrix[0].length;
        BIT = new int[m+1][n+1];
        nums = matrix;
                 
        //BIT creation
        createBIT(matrix);
    }
    
    public void update(int row, int col, int val) {
        int delta = val - nums[row] [col];
        nums[row][col] = val;
        updateBIT(delta, row+1, col+1);
    }
    
    public int sumRegion(int row1, int col1, int row2, int col2) {
        int sum = 0;
        int iMin = Math.min(row1, row2);
        int iMax = Math.max(row1, row2);
        int jMin = Math.min(col1, col2);
        int jMax = Math.max(col1, col2);
        
        //bottom right corner - top right corner - bottom left corner + common left top corner
        sum = getSum(iMax, jMax) - getSum(iMin-1,jMax) - getSum(iMax, jMin-1) + getSum(iMin-1, jMin-1); 
        return sum;
    }
    
    private void createBIT(int[][] matrix){
        for(int i = 1;i <= m;i++){
            for(int j = 1;j <= n; j++){
                updateBIT(matrix[i-1][j-1], i, j);
            }
        }
    }
    
    private void updateBIT(int val, int row, int col){
        
        for(int i = row; i< BIT.length; i = getNext(i)){
            for(int j = col; j< BIT[0].length ;j = getNext(j)){
                BIT[i][j] += val;
            }
        }
    }
    
    private int getSum(int row, int col){
        int sum = 0;
        row++; //index are always starting from 1...BIT.length
        col++;
        
        for(int i=row;i>0;i = getParent(i)){
            for(int j = col; j>0;j=getParent(j)){
                sum += BIT[i][j];
            }
        }
        
        return sum;
    }
    
    private int getParent(int index){
        return index - (index & -index);
    }
    
     private int getNext(int index){
        return index + (index & -index);
    }
}

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix obj = new NumMatrix(matrix);
 * obj.update(row,col,val);
 * int param_2 = obj.sumRegion(row1,col1,row2,col2);
 */
```
