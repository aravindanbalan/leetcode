Implement a trie with insert, search, and startsWith methods.

```java
public class Trie {

    /** Initialize your data structure here. */
    
    class TrieNode{
        char c;
        TrieNode[] children = new TrieNode[26]; //26 characters
        boolean isLeaf;
        TrieNode(){}
        TrieNode(char c){
            this.c = c;
        }
    }

    TrieNode root;
    
    public Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
         //we assume we dont store null or strings of length zero. 
        //We can also do that with some character say "$" or "#"
        if(word == null || word.length() == 0) return;
        
        TrieNode runner = root;
        
        for(char c : word.toCharArray()){
            if(runner.children[c-'a'] == null){
                //create the trie node
                runner.children[c-'a'] = new TrieNode(c);
            }
            runner = runner.children[c-'a'];
        }
        
        //last character
        runner.isLeaf = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        if(word == null || word.length() == 0) return false;
        
       TrieNode runner = root;
       for(char c : word.toCharArray()){
           if(runner.children[c-'a'] == null){
               return false;
           }else{
               runner = runner.children[c-'a'];
           }
       }
       //check if its a complete string
       return runner.isLeaf;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
         if(prefix == null || prefix.length() == 0) return false;
         
         TrieNode runner = root;
         for(char c : prefix.toCharArray()){
             if(runner.children[c-'a'] == null) return false;
             else runner = runner.children[c-'a'];
         }
         
         return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
