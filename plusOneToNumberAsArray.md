Given a non-negative integer represented as a non-empty array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

```java
public class Solution {
    public int[] plusOne(int[] digits) {
        int n = digits.length;
        for(int i = n-1; i>=0; i--){
            if(digits[i] == 9){
                digits[i] = 0;
            }else{
                digits[i]++;
                //we can return as this wont exceed 10 anymore
                return digits;
            }
        }
        if(digits[0] == 0){
            //which means its the corner case like 9 or 99 or 999 etc
            int[] res = new int[n+1];
            res[0] = 1;
            return res;
        }
        
        return digits;
    }
}
```
