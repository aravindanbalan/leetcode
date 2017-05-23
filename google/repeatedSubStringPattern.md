Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. 
You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.

```java
public class Solution {
    public boolean repeatedSubstringPattern(String s) {
        if(s == null || s.length() == 0) return false;
        
        StringBuilder sb = new StringBuilder();
        sb.append(s).append(s); //append s twice
        sb.deleteCharAt(0); //remove first character
        sb.deleteCharAt(sb.length()-1); //remove last character
        
        return sb.indexOf(s) != -1;
    }
}
```
