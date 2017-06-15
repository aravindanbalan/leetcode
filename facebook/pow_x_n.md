Implement pow(x, n).

```java

public class Solution {
    public double myPow(double x, int n) {
        if(x==0 || x == 1) return x;
        if(n==0) return 1;
        if(n==1) return x;
        
        //add 1 to n and later divide by x
        //this is to handle n = Integer.MIN_VALUE , idea is to make it Integer.Max_VALUE and then compute 
        //(-(n+1) makes it Integer.MAX_VALUE and for adding 1 we divide by x). -2147483648 becomes 2147483647
       if (n < 0) return 1.0/x/myPow(x, -(n+1));  // for handling case x = 2.000 and n = -2147483648
        
        if(n%2 == 0){
            return myPow(x*x,n>>1);
        }else{
            return myPow(x*x, n>>1) * x;
        }
    }
}
```
