Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

Note that 1 is typically treated as an ugly number

```java
public class Solution {
    public int nthUglyNumber(int n) {
        int min;
        int factor2=2, factor3=3, factor5 =5;
        int index2=0, index3=0, index5=0;
        
        int[] ugly = new int[n];
        ugly[0] = 1;
        for(int i=1;i<n;i++){
            min = Math.min(Math.min(factor2, factor3), factor5);
            ugly[i] = min;
            
            if(min == factor2)
                factor2 = 2 * ugly[++index2];
            if(min == factor3)
                factor3 = 3 * ugly[++index3];
            if(min == factor5)
                factor5 = 5 * ugly[++index5];
        }
        
        return ugly[n-1];
    }
}
```
