```
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

For example,
X X X X
X O O X
X X O X
X O X X
After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X
```

```java
public class Solution {
    public void solve(char[][] board) {
        
        
        // Idea is to capture all Os on the edges and change it to '+' since its not surrounded completely and will remain O.
        //they remain O in the end. add these points in the queue
        
        // then do a BFS with Os reachable from those points in queue and mark them +
        
        //in the end all + will become O
        //and other Os will become X
        
        int m = board.length;
        if(m == 0) return;
        int n = board[0].length;
        
        Queue<int[]> queue = new LinkedList<>();
        
        //for each row
        for(int i = 0; i< m ; i++){
            //left edge
            if(board[i][0] == 'O'){
                board[i][0] = '+';
                queue.add(new int[]{i, 0});
            }
            
            //right edge
            if(board[i][n-1] == 'O'){
                 board[i][n-1] = '+';
                queue.add(new int[]{i, n-1});
            }
        }
        
         //for each column
        for(int j = 0; j< n ; j++){
            //left edge
            if(board[0][j] == 'O'){
                board[0][j] = '+';
                queue.add(new int[]{0, j});
            }
            
            //right edge
            if(board[m-1][j] == 'O'){
                 board[m-1][j] = '+';
                queue.add(new int[]{m-1, j});
            }
        }
        
        //four directions
        int[][] dirs = {{-1, 0}, {1, 0}, {0,1}, {0, -1}};
        
        while(!queue.isEmpty()){
            int[] cell = queue.poll();
            
            for(int[] dir : dirs){
                int row = cell[0] + dir[0];
                int col = cell[1] + dir[1];
                
                //boundary check
                if(row < 0 || row >= m || col < 0 || col >=n ||
                board[row][col]!='O') continue;
                
                //address it
                board[row][col] = '+';
                queue.add(new int[]{row, col});
            }
        }
        
        
        //all + will become O
        //all O will become X as it will be surrounded
        for(int i = 0; i< m ;i++){
            for(int j = 0; j <n ;j++){
                if(board[i][j] == '+')
                    board[i][j] = 'O';
                else if(board[i][j] == 'O')
                    board[i][j] = 'X';
            }
        }
    }
}
```
