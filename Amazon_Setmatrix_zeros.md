Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

```java
public class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        
        boolean row = false, col = false;
        
        for(int i = 0; i< m ; i++){
            for(int j = 0; j < n ; j++){
                if(matrix[i][j] == 0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                    
                    if(i==0) row = true;
                    if(j == 0) col = true;
                }
            }
        }
        
        //starting from row 1 see if any of the values in col 0 is 0, then iterate thru that row elements and set everything zero
        for(int i = 1; i< m; i++){
            if(matrix[i][0] == 0){
                for(int j = 0 ; j< n; j++){
                    matrix[i][j] = 0;
                }
            }
        }
        
         //starting from col 1 see if any of the values in row 0 is 0, then iterate thru that col elements and set everything zero
        for(int j = 1; j< n; j++){
            if(matrix[0][j] == 0){
                for(int i = 0 ; i< m; i++){
                    matrix[i][j] = 0;
                }
            }
        }
        
        if(row){
            for(int j = 0 ; j< n ;j ++){
                matrix[0][j] = 0;
            }
        }
        
        if(col){
            for(int i = 0; i< m; i++){
                matrix[i][0] = 0;
            }
        }
    }
}
```
