Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2 as string.

```java

public class Solution {
    public String multiply(String num1, String num2) {
       if(num1 == null || num2 == null) return null;
       if(num1.length() == 0 || num2.length() == 0) return "0";
       
       
       int m = num1.length();
       int n = num2.length();
       int[] prod = new int[m+n];
       
       for(int i = m-1; i>=0;i--){
           for(int j = n-1; j>=0; j--){
               int mul = (num1.charAt(i) - '0') * (num2.charAt(j)-'0');
               int p1 = i+j;
               int p2 = i+j+1;
               int sum = mul + prod[p2];
               
               prod[p1] += sum /10;  //do not forget +=
               prod[p2] = sum % 10;
           }
       }
       
       StringBuilder sb = new StringBuilder();
       for(int num : prod) if(!(sb.length()==0 && num==0)) sb.append(num);   //only if sb is empty and num is zero then its a leading zero, so avoid it
       
       return sb.length()==0 ? "0" : sb.toString();
    }
}
```
