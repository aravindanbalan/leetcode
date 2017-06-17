```
The count-and-say sequence is the sequence of integers with the first five terms as following:

1.     1
2.     11
3.     21
4.     1211
5.     111221
1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.
```

```java
public class Solution {
    public String countAndSay(int n) {
        if(n <=0 ) return "-1";
        if(n == 1) return "1";
        
        String result = "1";
        for(int i = 1; i< n ; i++){
            result = countAndSayUtil(result);
        }
        
        return result;
    }
    
    private String countAndSayUtil(String result){
        int i = 0;
        StringBuilder sb = new StringBuilder();
        
        while(i < result.length()){
            char p = result.charAt(i);
            int count = 0;
            
            while(i < result.length() && p == result.charAt(i)){
                count++;
                i++;
            }
            sb.append(String.valueOf(count));
            sb.append(p);
        }
        
        return sb.toString();
    }
}
```
