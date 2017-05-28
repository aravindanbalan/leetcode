Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.

For example, given
s = "leetcode",
dict = ["leet", "code"].

Return true because "leetcode" can be segmented as "leet code".

```java
public class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        if(s == null || s.length() == 0 || wordDict == null || wordDict.size() == 0) return false;
        
        //let dp[i] represent whether a string from 0...i can be split into multiple words having all words in dict 
        boolean[] dp = new boolean[s.length()+1];
        dp[0] = true;
        Set<String> dict = new HashSet<String>();
        dict.addAll(wordDict);
        
        //cut at different places from 0 till i and then determine if it can be split
        for(int i = 1; i<= s.length() ; i++){
            //start to cut
            for(int j = 0; j< i ; j++){
                if(dp[j] && dict.contains(s.substring(j, i))){
                    dp[i] = true;
                }
            }
        }
        
        return dp[s.length()];
    }
}
```
