The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.



Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.

For example,
There exist two distinct solutions to the 4-queens puzzle:

```java
public class Solution {
    public List<List<String>> solveNQueens(int n) {
        if(n == 0) return new ArrayList<>();
        
        char[][] board = new char[n][n];
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j< n ; j++){
                board[i][j] = '.';
            }
        }
        
        List<List<String>> result = new ArrayList<List<String>>();
        solveNQueensUtil(board, 0, result);
        return result;
    }
    
    private void solveNQueensUtil(char[][] board, int colIndex, List<List<String>> result){
        if(colIndex == board.length){
            constructString(board, result);
            return;
        }
        
        for(int i = 0; i< board.length ; i++){
            if(isSafe(board, i, colIndex)){
                board[i][colIndex] = 'Q';
                solveNQueensUtil(board, colIndex+1, result);
                board[i][colIndex] = '.';
            }
        }
    }
    
    private boolean isSafe(char[][] board, int row, int col){
        for(int i = 0; i< board.length; i++){
            for(int j=0; j< col ; j++){ //since we are placing queens col by col and no need to check for the unexplored board which will all be safe anyways
                if(board[i][j] == 'Q' && ((row+j == col + i) || (row+col == i+j) || row==i)){
                    return false;
                }
            }
        }
        return true;
    }
    
    private void constructString(char[][] board, List<List<String>> result){
        List<String> temp = new LinkedList<String>();
         StringBuilder sb;
         
        for(int i = 0; i< board.length ; i++){
           sb = new StringBuilder();

            for(int j = 0; j< board.length; j++){
                sb.append(board[i][j]);
            }
            temp.add(sb.toString());
        }
        
        result.add(temp);
    }
}
```
