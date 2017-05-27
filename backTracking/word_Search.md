Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

For example,
Given board =

[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
word = "ABCCED", -> returns true,
word = "SEE", -> returns true,
word = "ABCB", -> returns false.

```java
public class Solution {
    public boolean exist(char[][] board, String word) {
        if(word == null || word.length() == 0 || board.length == 0 || board[0].length == 0) return false;
        
        int m = board.length;
        int n = board[0].length;
        boolean[][] visited = new boolean[m][n];
        
        //start from each cell
        for(int i = 0; i< m ;i++){
            for(int j = 0 ; j < n ;j++){
                if(word.charAt(0) == board[i][j] && wordSearchUtil(board, visited, m, n, word, i, j, 0)){
                    return true;
                }
            }
        }
        
        return false;
    }
    
    private boolean wordSearchUtil(char[][] board, boolean[][] visited, int m, int n, String word, int row, int col, int index){
        if(index == word.length()) return true;
        
        if(row < 0 || row >= m || col < 0 || col>=n || visited[row][col] || board[row][col]!=word.charAt(index)) 
            return false;
        
        visited[row][col] = true;

        //all four directions
        int[][] dirs = {{-1, 0}, {1, 0}, {0, 1}, {0,-1}};
        
        for(int[] dir : dirs){
            int i = dir[0] + row;
            int j = dir[1] + col;
        
            if(wordSearchUtil(board, visited, m, n, word, i, j, index+1)){
                return true;
            }
        }
        
        visited[row][col] = false;
        
        return false;
    }
}
```
