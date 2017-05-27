Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

For example,
Given words = ["oath","pea","eat","rain"] and board =

[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
Return ["eat","oath"].

```java
public class Solution {
    class TrieNode{
        char c;
        TrieNode[] children = new TrieNode[26];
        boolean isLeaf;
        
        TrieNode(){}
        TrieNode(char c){
            this.c = c;
        }
    }
    
    public List<String> findWords(char[][] board, String[] words) {
        if(words.length == 0 || board.length == 0 || board[0].length == 0) return new ArrayList<>();
        int m = board.length;
        int n = board[0].length;
        
        TrieNode root = new TrieNode();
        
        for(String word : words){
            insert(root, word);
        }
        
        boolean[][] visited = new boolean[m][n];
        Set<String> result = new HashSet<String>();
        for(int i = 0 ; i< m ; i++){
            for(int j = 0; j< n ; j++){
                if(root.children[board[i][j] - 'a'] != null)
                    findWordsUtil(board, m , n, i, j, result, root, "", visited);
            }
        }
        
        return new LinkedList<String>(result);
    }
    
    private void findWordsUtil(char[][] board, int m , int n, int row, int col, Set<String> result, TrieNode runner, String str, boolean[][] visited){
        
        //if already visited or boundary check
        if(row < 0 || row >=m || col < 0 || col >= n || visited[row][col]) return;
        
        //if character at row col is not there in trie;
        char c = board[row][col];
        if(runner.children[c - 'a'] == null) return;
        
        str += c;
        if(runner.children[c-'a'].isLeaf){
            result.add(str);
        }
        
        visited[row][col] = true;
        
        //all four directions
        int[][] dirs = {{-1, 0}, {1, 0}, {0, 1}, {0, -1}};
        
        for(int[] dir : dirs){
            int i = dir[0] + row;
            int j = dir[1] + col;
            
            findWordsUtil(board, m , n, i, j, result, runner.children[c-'a'], str, visited);
        }
        
        visited[row][col] = false;
    }
    
    private void insert(TrieNode root, String word){
        if(word == null || word.length() == 0) return;
        
        TrieNode runner = root;
        
        for(char c : word.toCharArray()){
            if(runner.children[c-'a'] == null){
                runner.children[c-'a'] = new TrieNode(c);
            }
            
            runner = runner.children[c-'a'];
        }
        
        runner.isLeaf = true;
    }
    
    
}
```
