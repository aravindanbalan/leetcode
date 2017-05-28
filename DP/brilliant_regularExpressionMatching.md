Implement regular expression matching with support for '.' and '*'.

'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        if(s == null && p== null) return true;
        if(s == null || p == null) return false;
        
        //dp solution
        boolean[][] dp = new boolean[s.length() +1][p.length()+1];
        dp[0][0] = true;
        
        //for patterns like a*, a*b*, a*b*c* and s = ""  -> these are matches
        for(int i = 1; i<= p.length() ;i++){
           if(p.charAt(i-1) == '*'){
               dp[0][i] = dp[0][i-2];
           }
        }
        
        for(int i = 1; i <= s.length() ; i++){
            for(int j = 1; j<= p.length() ; j++){
                if(s.charAt(i-1) == p.charAt(j-1) || p.charAt(j-1) == '.'){
                    //same characters match
                    dp[i][j] = dp[i-1][j-1];
                }
                else if(p.charAt(j-1) == '*'){
                    dp[i][j] = dp[i][j-2]; // zero occurences of 'a' s= x, p = xa*
                    
                    if(p.charAt(j-2) == '.' || s.charAt(i-1) == p.charAt(j-2)){
                        dp[i][j] = dp[i][j] || dp[i-1][j]; //one occurence of a s= xa , p = xa* or s = xa , p = .a*
                    }
                }
            }
        }
        
        return dp[s.length()][p.length()];
        
    }

}
```
