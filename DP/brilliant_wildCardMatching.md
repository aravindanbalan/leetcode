Implement wildcard pattern matching with support for '?' and '*'.

'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false

```java
public class Solution {
    public boolean isMatch(String s, String p) {
         if(s == null && p== null) return true;
        if(s == null || p == null) return false;

        //handle s="" and p = ""
        if(s.length() == 0 && p.length() == 0) return true;
        
        char[] str = s.toCharArray();
        char[] pattern = p.toCharArray();
        
        //replace multiple * with one *
        //e.g a**b***c --> a*b*c
        int writeIndex = 0;
        boolean isFirst = true;
        for ( int i = 0 ; i < pattern.length; i++) {
            if (pattern[i] == '*') {
                if (isFirst) {
                    pattern[writeIndex++] = pattern[i];
                    isFirst = false;
                }
            } else {
                pattern[writeIndex++] = pattern[i];
                isFirst = true;
            }
        }
        
        boolean[][] dp = new boolean[s.length() +1][writeIndex +1];
        dp[0][0] = true;
        
        //after compression from ***** to *
        if (writeIndex > 0 && pattern[0] == '*') {
            dp[0][1] = true;
        }
        
        for(int i= 1; i<= str.length;i++){
            for(int j = 1; j<=writeIndex; j++){
                
                if(str[i-1] == pattern[j-1] || pattern[j-1] == '?'){
                    dp[i][j] = dp[i-1][j-1];
                }else if(pattern[j-1] == '*'){
                    dp[i][j] = dp[i][j-1] || dp[i-1][j]; //zero or 1 occurrence of any character
                }
            }
        }
        
        return dp[s.length()][writeIndex];
    }
}
```
