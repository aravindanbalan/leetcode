Design a data structure that supports the following two operations:

void addWord(word)
bool search(word)
search(word) can search a literal word or a regular expression string containing only letters a-z or .. A . means it can represent any one letter.

```java
public class WordDictionary {
    
    class TrieNode{
        char c;
        TrieNode[] children = new TrieNode[26];
        boolean isLeaf;
        TrieNode(){}
        TrieNode(char c){
            this.c = c;
        }
    }

    TrieNode root;
    /** Initialize your data structure here. */
    public WordDictionary() {
        root = new TrieNode();
    }
    
    /** Adds a word into the data structure. */
    public void addWord(String word) {
        //we assume we dont store null or strings of length zero. 
        //We can also do that with some character say "$" or "#"
        if(word == null || word.length() == 0) return;
        
        TrieNode runner = root;
        for(char c : word.toCharArray()){
            if(runner.children[c-'a'] == null){
                runner.children[c-'a'] = new TrieNode(c);
            }
            
            runner = runner.children[c-'a'];
        }
        
        //last character
        runner.isLeaf = true;
    }
    
    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    public boolean search(String word) {
        if(word == null || word.length() == 0) return false;
        return match(word.toCharArray(), 0, root); 
    }
    
    //use recursion
    private boolean match(char[] word, int index, TrieNode runner){
        if(index == word.length) return runner.isLeaf;
        
        char c = word[index];
        if(c != '.'){
            return runner.children[c-'a']!=null && match(word, index+1, runner.children[c-'a']);
        }else{
            
            //iterate and find the non null children and do a bfs for each
            for(int i = 0; i < 26 ;i++){
                if(runner.children[i]!=null){
                    if(match(word, index+1, runner.children[i])){
                        return true;
                    }
                }
            }
        }
        
        return false;
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```
