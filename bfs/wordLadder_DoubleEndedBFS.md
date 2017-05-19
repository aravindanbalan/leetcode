```
Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

Only one letter can be changed at a time.
Each transformed word must exist in the word list. Note that beginWord is not a transformed word.
For example,

Given:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log","cog"]
As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5
```

```java
public class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        if(beginWord == null || endWord == null || wordList == null || wordList.size() == 0) return 0;
        //we can do normal BFS
        
        // Queue<String> queue = new LinkedList<String>();
        // Set<String> dict = new HashSet<String>(wordList);
        // Set<String> visited = new HashSet<String>();
        // visited.add(beginWord);
        
        // queue.add(beginWord);
        
        // int len = 1; //start word
        // while(!queue.isEmpty()){
        //     len++;

        //     String word = queue.poll();
            
        //     char[] wordChar = word.toCharArray();
        //     for(int i = 0; i< wordChar.length; i++){
        //         //for each position in the word
                
        //         for(char c = 'a' ; c <= 'z' ; c++){
        //             wordChar[i] = c;
        //             String newWord = new String(wordChar);
                    
        //             if(endWord.equals(newWord)) return len + 1; //including the end word itself
                    
        //             if(!visited.contains(newWord) && dict.contains(newWord)){
        //                 visited.add(newWord);
        //                 queue.add(newWord);
        //             }
                
        //         }
        //     }
        // }
        
        // return 0;
        
        
        //we can do double ended BFS - faster than normal BFS
        
        Set<String> wordDict = new HashSet<String>(wordList);

        //if end word is not in dictionary then we cant find a solution
        if(!wordDict.contains(endWord)) return 0;
        
        int len = 1;
        Set<String> beginSet = new HashSet<>();
        Set<String> endSet = new HashSet<>();
        Set<String> visited = new HashSet<>();
        
        beginSet.add(beginWord);
        endSet.add(endWord);
        visited.add(beginWord);
        visited.add(endWord);
        
        while (!beginSet.isEmpty() && !endSet.isEmpty()) {
            // add new words to smaller set to achieve better performance
            boolean isBeginSetSmall = beginSet.size() < endSet.size();
            Set<String> small = isBeginSetSmall ? beginSet : endSet;
            Set<String> big = isBeginSetSmall ? endSet : beginSet;
            Set<String> next = new HashSet<>();
            len++;
            for (String str : small) {
                // construct all possible words
                for (int i = 0; i < str.length(); i++) {
                    for (char ch = 'a'; ch <= 'z'; ch++) {
                        StringBuilder sb = new StringBuilder(str);
                        sb.setCharAt(i, ch);
                        String word = sb.toString();
                        if (big.contains(word)) {
                            return len;
                        }
                        if (wordDict.contains(word) && !visited.contains(word)) {
                            visited.add(word);
                            next.add(word);
                        }
                    }
                }
            }
            if (isBeginSetSmall) {
                beginSet = next;
            } else {
                endSet = next;
            }
        }
        return 0;
    }
}
```
