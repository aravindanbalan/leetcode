```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        if(n==0 || n==1) return n;
        
        // int count = 0;
        // for (int i=0;i<32;i++) count += (n >> i) & 1;
        
        // return count;
        
        
        //java api
        return Integer.bitCount(n);
    }
}
```
