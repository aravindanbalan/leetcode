Implement regular expression matching with support for '.' and '*'.

'.' Matches any single character.
'*' Matches zero or more characters.

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        if(s == null && p== null) return true;
        if(s == null || p == null) return false;
        if(s.equals(p)) return true;
        
        return isMatchUtil(s, 0, p , 0);
    }
    
    private boolean isMatchUtil(String s, int i, String p, int j){
        if(i == s.length() && j < p.length()){
            return false; //reached end of original string without matching
        }
        
        if(j == p.length()) return (i == s.length());
        
        if(p.charAt(j) == '*'){
            return isMatchUtil(s, i+1, p, j+1) || isMatchUtil(s, i+1, p, j);
        }else if(p.charAt(j) == '.'){
            return isMatchUtil(s, i+1, p, j+1);
        }else{
            return (s.charAt(i) == p.charAt(j)) && isMatchUtil(s, i+1, p, j+1);
        }
    }
}
```
