Determine if a Sudoku is valid, according to: Sudoku Puzzles - The Rules.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

```java
public class Solution {
    public boolean isValidSudoku(char[][] board) {
        if(board.length == 0 || board[0].length == 0) return true;
        
        //for each row and column
        for(int i = 0; i<=8 ;i++){
            //each row
            if(!isValidUtil(board, i, 0, i, 8)) return false;
            //each col
            if(!isValidUtil(board, 0, i, 8, i)) return false;
        }
        
        //each cube
        //each cube starts at (i*3, j*3) away and ends at (i*3 +2, j*3 +2)
        for(int i = 0; i<3; i++){
            for(int j = 0; j<3;j++){
                if(!isValidUtil(board, i*3, j*3, i*3+2, j*3+2)) return false;
            }
        }
        
        return true;
    }
    
    //checks for all cells from x1 to x2 and y1 to y2
    private boolean isValidUtil(char[][] board, int x1, int y1, int x2, int y2){
        Set<Integer> set = new HashSet<Integer>();
        
        for(int i = x1; i<= x2; i++){
            for(int j= y1; j <= y2; j++){
                if(board[i][j] != '.'){
                    
                    //set.add() returns false if the element is already present
                    if(!set.add(board[i][j] - 'a')) return false;
                }
            }
        }
        
        return true;
    }
}
```
