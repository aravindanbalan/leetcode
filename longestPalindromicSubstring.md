Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example:

Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.
Example:

Input: "cbbd"

Output: "bb"

```java
public class Solution {
    public String longestPalindrome(String s) {
        if(s == null || s.length() == 0){
            return s;
        }
        
        int n = s.length();
        boolean[][] table = new boolean[n][n];
        
        int maxLength=1;
        for(int i =0;i<n;i++){
            table[i][i] = true;  //string of length 1 are palindromes
        }
        
        int start = 0;

        for(int i =0;i < n-1 ;i++){
            if(s.charAt(i) == s.charAt(i+1)){
                table[i][i+1] = true;
                start = i;
                maxLength = 2;
            }
        }
        
        for(int k = 3 ; k<=n ;k++){
            for(int i =0;i< n-k+1;i++){
                int j = i+k-1;
                
                if(table[i+1][j-1] && s.charAt(i) == s.charAt(j)){
                    table[i][j] = true; //i..j is also a palindrome
                    
                    if(k > maxLength){
                        maxLength = k;
                        start = i; //update starting index and length
                    }
                }
            }
        }
        
        return s.substring(start, start+ maxLength);
    }
}
```
