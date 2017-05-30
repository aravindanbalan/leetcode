```java
public class Solution {
    
    //DFS solution
    int[][] dirs = {{-1,0}, {-1,1}, {-1, -1}, {0, 1}, {0, -1}, {1, 0}, {1, 1}, {1, -1}};
    public char[][] updateBoard(char[][] board, int[] click) {
        int x = click[0];
        int y = click[1];
        
        if(board[x][y] == 'M'){
            board[x][y] = 'X'; //unreveal mine and game over
            return board;
        }
        
        //recursively update board
        int m = board.length;
        int n = board[0].length;
        updateBoardUtil(board, x, y, m, n);
        return board;
    }
    
    private void updateBoardUtil(char[][] board, int row, int col, int m, int n){
        //boundary check for recursion
        if(row < 0 || row >=m || col < 0 || col >=n || board[row][col] != 'E') return;
        
        int count = getSurroundingMines(board, row, col, m, n);
        
        //if no mines then set current cell to blank and then reveal recursively
        if(count == 0){
            board[row][col] = 'B'; //reveal
            
            for(int[] dir : dirs){
                int i = dir[0] + row;
                int j = dir[1] + col;
                
                //call recursively
                updateBoardUtil(board, i, j, m , n);
            }
        }else{
            //set the corresponding mine count number
            board[row][col] = (char)('0' + count);
        }
    }
    
    private int getSurroundingMines(char[][] board, int row, int col, int m, int n){
        //check all 8 directions
        int count = 0;
        for(int[] dir : dirs){
            int i = dir[0] + row;
            int j = dir[1] + col;
            
            if(i < 0 || i >=m || j < 0 || j >=n ) continue;
            
            //either a revealed or unrevealed mine
            if(board[i][j] == 'M' || board[i][j] == 'X') count++;

        }
        return count;
    }
}
```
