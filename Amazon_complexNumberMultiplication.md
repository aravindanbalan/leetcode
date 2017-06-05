```
Given two strings representing two complex numbers.

You need to return a string representing their multiplication. Note i2 = -1 according to the definition.

Example 1:
Input: "1+1i", "1+1i"
Output: "0+2i"
Explanation: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i, and you need convert it to the form of 0+2i.
Example 2:
Input: "1+-1i", "1+-1i"
Output: "0+-2i"
Explanation: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i, and you need convert it to the form of 0+-2i.
```
```java

public class Solution {
    public String complexNumberMultiply(String a, String b) {
        int[] valA = getValues(a);
        int[] valB = getValues(b);
        
        int real = valA[0] * valB[0] - valA[1] * valB[1]; //first two values, - is for i^2 , second two values
        int img = valA[0] * valB[1] + valA[1] * valB[0];
        
        return "" + real + "+" + img + "i";
    }
    
    private int[] getValues(String s){
        String[] str = s.split("\\+");
        
        int[] val = new int[2];
        val[0] = Integer.parseInt(str[0]);
        
        int index = str[1].indexOf("i");
        val[1] = Integer.parseInt(str[1].substring(0, index));
        return val;
    }
}
```
