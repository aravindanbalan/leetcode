Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

Example 1:
Input:

"bbbab"
Output:
4

```java
public class Solution {
    public int longestPalindromeSubseq(String s) {
        //We can solve this in DP
        
        if(s == null || s.length() == 0) return 0;
        
        int[][] dp = new int[s.length()][s.length()];
        //let dp[i][j] denote the length of longest palindrom subseq from i...j
        
        for(int i = s.length() -1; i >=0; i--){
            dp[i][i] = 1; //single character is also a palindrome
            
            for(int j = i+1;j < s.length(); j++){
                if(s.charAt(i) == s.charAt(j)){
                    dp[i][j] = dp[i+1][j-1] + 2;
                }else{
                    dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
                }
            }
        }
        
        return dp[0][s.length()-1];
    }
}
```
