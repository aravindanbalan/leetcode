```java
public class Solution {
    public int divide(int dividend, int divisor) {
         if (divisor ==0 || (dividend == Integer.MIN_VALUE && divisor == -1))
            return Integer.MAX_VALUE;
            
        int res = 0;

        if(dividend == divisor) return 1;
        
        if(divisor == 1) return dividend;

        if(dividend < divisor) return 0;
        
        int sign = ((dividend <0 && divisor >0) || (dividend > 0 && divisor < 0)) ? -1 : 1;
        
        dividend = Math.abs(dividend);
        divisor = Math.abs(divisor);
        
        int div = divisor;
        
        while(dividend >= div){
            int quotient = 1;
            int tempDiv = div;
            
            while(dividend >= (tempDiv<<1)){
                tempDiv<<=1;
                quotient<<=1;
            }
            
            res+= quotient;
            dividend -= tempDiv;
        }
        
        return sign * res;
    }
}
```
