Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

```java
public class Solution {
    public int myAtoi(String str) {
        if(str == null){
            return 0;
        }
    
        //trim spaces first
       str = str.trim();
       
       if(str.length() == 0) return 0;
       int sign = 1;
      
        
        if (str.charAt(0) == '-' || str.charAt(0) == '+') {
            sign = (str.charAt(0) == '-') ? -1 : 1;
            str = str.substring(1);
        }
        
        int n = str.length();
     
        int base = 0;
        int i = 0;
        while(i< n && (str.charAt(i) >= '0' && str.charAt(i) <='9')){
            if(base > (Integer.MAX_VALUE / 10) || (base == Integer.MAX_VALUE/10 && str.charAt(i)-'0' > 7)){
                return (sign < 0) ? Integer.MIN_VALUE : Integer.MAX_VALUE;
            }
            base = 10*base + (int)(str.charAt(i) - '0');
            i++;
        }
        
        return sign * base;
    }
}
```
