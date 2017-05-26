Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.

```java
public class Solution {
    public String intToRoman(int num) {
        
        //Very simple
        // I : 1 , V - 5, X : 10, L = 50, C = 100, D = 500, M = 1000
        
        //since 4, 9, 40, 90 , 400, 900 are special cases, we can store them in array along with 1, 5, 10, 100, 500, 1000
        
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] roman = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
        
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i< values.length; i++){
            //for each of the values, reduce number such that it falls inside each bucket
            while(num >= values[i]){
                num -= values[i]; //say 3300, we need 3 Ms (MMM), first then CCC
                sb.append(roman[i]);  //append roman equivalent
            }
        }
        
        return sb.toString();
    }
}
```
