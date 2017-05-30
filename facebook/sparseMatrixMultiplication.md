```java
public class Solution {
    public int[][] multiply(int[][] A, int[][] B) {
        //Simple solution
        
        int m = A.length; int n = A[0].length; int nB = B[0].length;
        int[][] c = new int[m][nB];
        
        for(int i = 0; i< m;i++){
            for(int k = 0; k < n;k++){
                if(A[i][k]!=0){
                    for(int j = 0; j < nB; j++){
                        c[i][j] += A[i][k] * B[k][j];
                    }
                }
            }
        }
        return c;
        
        
        //Another idea is to convert A into a sequence of rows with only non zero values
        // A = List[m] for each row and each one is an arraylist{col, val}
        
    }
}
```

