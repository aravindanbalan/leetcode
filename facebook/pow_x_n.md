Implement pow(x, n).

```java

public class Solution {
    public double myPow(double x, int n) {
        if(x==0 || x == 1) return x;
        if(n==0) return 1;
        if(n==1) return x;
        
        //add 1 to n and later divide by x
        //this is to handle n = Integer.MIN_VALUE , 
        //In java max = 2^31-1 , min = -2^31
        
        //so if we do -min then it becomes 2^31 and we cant hold that value in Integer, so to convert it to Integer.MAX_VALUE we do
        // - (n+1) = - (-2^31 + 1) = 2^31 - 1 = Max
        
       if (n < 0) return 1.0/x/myPow(x, -(n+1));  // for handling case x = 2.000 and n = -2147483648
        
        if(n%2 == 0){
            return myPow(x*x,n>>1);
        }else{
            return myPow(x*x, n>>1) * x;
        }
    }
}
```
