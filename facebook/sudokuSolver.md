Write a program to solve a Sudoku puzzle by filling the empty cells.

Empty cells are indicated by the character '.'.

You may assume that there will be only one unique solution.

```java
public class Solution {
    public void solveSudoku(char[][] board) {
        if(board.length == 0 || board[0].length == 0) return;
        solveUtil(board);
    }
    
    private boolean solveUtil(char[][] board){
         //we need to scan through each cell of the board to find an empty cell
        for(int i= 0; i<9; i++){
            for(int j = 0; j<9; j++){
                if(board[i][j] == '.'){
                    
                    //all possible values that can be placed in this cell
                    for(char c = '1' ; c<='9'; c++){
                       
                       //only if its valid to place it in this cell, place it
                       if(isValid(board, i, j, c)){
                        //place it in this empty cells
                        board[i][j] = c;
                        
                        if(solveUtil(board)){
                            return true;
                        }
                        
                        board[i][j] = '.'; //backtracking, make it unassigned again
                       }
                    }
                    
                    return false;
                }
            }
        }
        
        //we have a solution if we reach here, since no empty cells anymore
        return true;
    }
    
    private boolean isValid(char[][] board, int row, int col, char c){
        
        //check for each value in row, col and that cell
        for(int i = 0; i< 9; i++){
            
            //check all values in that col where you placed
            if(board[i][col] != '.' && board[i][col] == c) return false;
            
            //check all values in that row where you placed
            if(board[row][i] != '.' && board[row][i] == c) return false;
            
            int cellRow = 3*(row/3) + i/3;
            int cellCol = 3*(col/3) + i%3;
            
            if(board[cellRow][cellCol] != '.' && board[cellRow][cellCol] == c) return false;
            
        }
        
        return true;
    }
}
```
