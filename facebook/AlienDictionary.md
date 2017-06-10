```
There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

Example 1:
Given the following words in dictionary,

[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]
The correct order is: "wertf".

Example 2:
Given the following words in dictionary,

[
  "z",
  "x"
]
The correct order is: "zx".

Example 3:
Given the following words in dictionary,

[
  "z",
  "x",
  "z"
]
```

```java
public class Solution {
    public String alienOrder(String[] words) {
        if(words.length == 0) return "";
        
        //lets maintain the indegree of each character
        Map<Character, Integer> indegree = new HashMap<Character, Integer>();
        Map<Character, Set<Character>> edges = new HashMap<Character, Set<Character>>();
        
        for(String word : words){
            for(char c : word.toCharArray()){
                indegree.put(c, 0); //get all unique chars in all words
            }
        }
        
        //process words in pairs
        for(int i = 0; i< words.length - 1; i++){
            String word1 = words[i];
            String word2 = words[i+1];
            
            int len = Math.min(word1.length() , word2.length());
            
            for(int j = 0; j< len ; j++){
                char c1 = word1.charAt(j);
                char c2 = word2.charAt(j);
                
                if(c1!=c2){
                    Set<Character> set = new HashSet<Character>();
                    
                    if(edges.containsKey(c1)) set = edges.get(c1);
                    
                    if(!set.contains(c2)){
                        set.add(c2);
                        edges.put(c1, set); //update adjacency list
                        //udpate indegree for c2
                        indegree.put(c2, indegree.get(c2) + 1);
                    }
                    break; //do it only till you get a unequal character
                }
            }
        }
        
        StringBuilder sb  = new StringBuilder();
        
        Queue<Character> queue = new LinkedList<Character>();
        
        for(char c : indegree.keySet()){
            if(indegree.get(c) == 0) queue.add(c);
        }
        
        while(!queue.isEmpty()){
            char c = queue.poll();
            sb.append(c);
            
            if(edges.containsKey(c)){
                for(char c2 : edges.get(c)){
                    //reduce indegree of its adjacent nodes by 1
                    indegree.put(c2, indegree.get(c2) -1);
                    if(indegree.get(c2) == 0) queue.add(c2);
                }
            }
        }
        
        //because all characters needs to be there in topological ordering. Similar to classes pre-requisities problem.
        if(sb.length()!=indegree.size()) return "";
        return sb.toString();
    }
}
```
