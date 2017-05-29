Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, add spaces in s to construct a sentence where each word is a valid dictionary word. You may assume the dictionary does not contain duplicate words.

Return all such possible sentences.

For example, given
s = "catsanddog",
dict = ["cat", "cats", "and", "sand", "dog"].

A solution is ["cats and dog", "cat sand dog"].



```java
public class Solution {
    Map<String, List<String>> map = new HashMap<String, List<String>>();
    public List<String> wordBreak(String s, List<String> wordDict) {
        //DFS 
        Set<String> set = new HashSet<String>();
        set.addAll(wordDict);
        return wordBreakUtil(s, set);
    }
    
    private List<String> wordBreakUtil(String s, Set<String> wordDict){
        List<String> result = new LinkedList<String>();
        if(s == null || s.length() == 0){
            return result;
        }
        
        if(map.containsKey(s)){
            return map.get(s);
        }
        
        if(wordDict.contains(s)){
            result.add(s);
        }
        
        //cut from 1
        for(int j = 1; j< s.length() ; j++){
            String t = s.substring(j);
            //if second part is in dict then process first part recursively in dfs call
            if(wordDict.contains(t)){
                List<String> res = wordBreakUtil(s.substring(0, j), wordDict);
                if(res.size()!=0){
                    for(String str: res){
                        result.add(str + " " + t);
                    }
                }
            }
        }
        
        map.put(s, result);
        return result;
    }
}
```
