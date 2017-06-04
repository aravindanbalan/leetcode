```
Given two words (beginWord and endWord), and a dictionary's word list, find all shortest transformation sequence(s) from beginWord to endWord, such that:

Only one letter can be changed at a time
Each transformed word must exist in the word list. Note that beginWord is not a transformed word.
For example,

Given:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log","cog"]
```

```java
public class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        if(beginWord == null || endWord == null || wordList.size() == 0) return new ArrayList<>();
        
        //Idea is to use both bfs and dfs
        Set<String> dict = new HashSet<String>(wordList);
        List<List<String>> result = new ArrayList<>();
        Map<String, Integer> distance = new HashMap<>();
        Map<String, List<String>> nodeNeighbors = new HashMap<String, List<String>>();
       
       dict.add(beginWord);
       bfs(beginWord, endWord, distance, nodeNeighbors, dict);
       dfs(beginWord, endWord, distance, nodeNeighbors, new ArrayList<String>(), result);
       return result;
    }
    
    private void bfs(String beginWord, String endWord, Map<String, Integer> distance, Map<String, List<String>> nodeNeighbors, Set<String> dict){
        
        Queue<String> queue = new LinkedList<String>();
        queue.add(beginWord);
        distance.put(beginWord, 0);
        
        //add empty list for all words in dict to store all the neighbors or each of the words in dict
        for(String str : dict){
            nodeNeighbors.put(str, new ArrayList<String>());
        }
        
        while(!queue.isEmpty()){
            int count = queue.size();
            
            //level order traversal
            for(int i = 0; i< count ; i++){
                String curr = queue.poll();
                int currdist = distance.get(curr);
                
                List<String> neighbors = getNeighbors(curr, dict);
                
                //for each of its neighbors
                for(String neighbor : neighbors){
                    nodeNeighbors.get(curr).add(neighbor);
                    
                    //if it was already visited that would have been the shortest distance as we are doing level order traversal
                    if(!distance.containsKey(neighbor)){ 
                        distance.put(neighbor, currdist + 1);
                        
                        //add to queue only when endword is not reached otherwise its a waste again to continue
                        if(!endWord.equals(neighbor)){
                            queue.add(neighbor);
                        }
                    }
                }
            }
        }
    }
    
    private List<String> getNeighbors(String word, Set<String> dict){
        char[] ch = word.toCharArray();
        List<String> result = new ArrayList<String>();
        
        for(int i =0; i< ch.length ; i++){
            
            for(char c = 'a' ; c <= 'z'; c++){
                char old = ch[i];
                ch[i] = c;
                
                String newWord = new String(ch);
                if(dict.contains(newWord)){
                    result.add(newWord);
                }
                ch[i] = old;
            }
        }
        
        return result;
    }
    
    private void dfs(String currWord, String endWord, Map<String, Integer> distance, Map<String, List<String>> nodeNeighbors, List<String> tempList, List<List<String>> result){
        tempList.add(currWord);
        
        if(endWord.equals(currWord)){
            result.add(new ArrayList(tempList));
        }else{
            
            List<String> neighBors = nodeNeighbors.get(currWord);
            for(String neighbor : neighBors){
                if(distance.get(neighbor) == distance.get(currWord) + 1){ //only if distance is by 1 character then proceed
                   dfs(neighbor, endWord, distance, nodeNeighbors, tempList, result);
                }
            }
        }
        
        tempList.remove(tempList.size() - 1);
    }

}
```
