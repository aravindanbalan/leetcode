Given an array of integers A and let n to be its length.

Assume Bk to be an array obtained by rotating the array A k positions clock-wise, we define a "rotation function" F on A as follow:

F(k) = 0 * Bk[0] + 1 * Bk[1] + ... + (n-1) * Bk[n-1].

Calculate the maximum value of F(0), F(1), ..., F(n-1).



```java
public class Solution {
    public int maxRotateFunction(int[] A) {
        if(A.length == 0){
            return 0;
        }
        
        
        int sum = 0;
        int n = A.length;
        int F = 0; //initially represents F[0]
        
        for(int i = 0; i< n; i++){
            F += i * A[i];
            sum += A[i];
        }
        
        int max = F;

        for(int k = n-1; k>=1;k--){
            F += sum  - (n * A[k]);
            max = Math.max(max, F);
        }
        
        return max;
    }
    
    /**
     * F(k) = 0 * Bk[0] + 1 * Bk[1] + ... + (n-1) * Bk[n-1]
        F(k-1) = 0 * Bk-1[0] + 1 * Bk-1[1] + ... + (n-1) * Bk-1[n-1]
               = 0 * Bk[1] + 1 * Bk[2] + ... + (n-2) * Bk[n-1] + (n-1) * Bk[0]
        Then,
        
        F(k) - F(k-1) = Bk[1] + Bk[2] + ... + Bk[n-1] + (1-n)Bk[0]
                      = (Bk[0] + ... + Bk[n-1]) - nBk[0]
                      = sum - nBk[0]
        Thus,
        
        F(k) = F(k-1) + sum - nBk[0]
        What is Bk[0]?
        
        k = 0; B[0] = A[0];
        k = 1; B[0] = A[len-1];
        k = 2; B[0] = A[len-2];
        ...
     * */
}
```
