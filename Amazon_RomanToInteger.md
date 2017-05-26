```java
public class Solution {
    public int romanToInt(String s) {
        if(s == null || s.length() == 0) return 0;
        
        //we have special cases where its reverse
        //IV - 4, IX - 9, 40 - XL, 90 - XC, 400 - CD, 900 - CM
        
        //if we add I + V = 6 - 2 = 4 for special case alone
        //if we add I + X = 11 - 2 = 9
        //if we add X + L = 60 - 20 = 40
        //X + C = 110 - 20 = 90
        //C + D = 600 - 200 = 400
        // C + M = 1100 - 200 = 900
        
        //rest we can just add from left to right
        
        int sum = 0;
        //preprocess
        if(s.indexOf("IV")!=-1) sum -=2;
        if(s.indexOf("IX")!=-1) sum-=2;
        if(s.indexOf("XL")!=-1) sum-=20;
        if(s.indexOf("XC")!=-1) sum-=20;
        if(s.indexOf("CD")!=-1) sum-=200;
        if(s.indexOf("CM")!=-1) sum -= 200;
        
        for(int i = 0; i< s.length(); i++){
            switch(s.charAt(i)){
                case 'I':
                    sum+=1;
                    break;
                case 'V':
                    sum += 5;
                    break;
                case 'X':
                    sum+= 10;
                    break;
                case 'L':
                    sum += 50;
                    break;
                case 'C':
                    sum += 100;
                    break;
                case 'D':
                    sum += 500;
                    break;
                case 'M':
                    sum += 1000;
                    break;
            }
        }
    
        return sum;
    }
}
```
