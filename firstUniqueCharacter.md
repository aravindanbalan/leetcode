```java

public class Solution {
    public int firstUniqChar(String s) {
        if(s == null || s.length() == 0)
            return -1;
        if(s.length() == 1){
            return 0;
        }
        
        int[] frequency = new int[26];
        
        for(char c : s.toCharArray()){
            frequency[c-'a']++;
        }
        
          for(int i =0;i< s.length() ;i++){
            if(frequency[s.charAt(i) - 'a'] == 1) return i;  
          }
          
          return -1;
    }
}
```
