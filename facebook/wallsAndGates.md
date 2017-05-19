```
You are given a m x n 2D grid initialized with these three possible values.

-1 - A wall or an obstacle.
0 - A gate.
INF - Infinity means an empty room. We use the value 231 - 1 = 2147483647 to represent INF as you may assume that the distance to a gate is less than 2147483647.
Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.

For example, given the 2D grid:
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
After running your function, the 2D grid should be:
  3  -1   0   1
  2   2   1  -1
  1  -1   2  -1
  0  -1   3   4
```

```java
public class Solution {
    public void wallsAndGates(int[][] rooms) {
        
        /**
         * Mantra : If we are asked distance to gates, always do BFS and start by adding the gates and start updating the distances to nearby cells
         */
        
        int m = rooms.length;
        if(m == 0) return;
        int n = rooms[0].length;
        
        Queue<int[]> queue = new LinkedList<>();
        
        for(int i = 0; i< m ;i++){
            for(int j = 0; j< n ;j++){
                if(rooms[i][j] == 0){
                    queue.add(new int[]{i, j});
                }
            }
        }
        
        //all four directions
        int[][] dirs = {{-1,0}, {1, 0}, {0, 1}, {0, -1}};
        while(!queue.isEmpty()){
            int[] cell = queue.poll();
            
            for(int[] dir : dirs){
                int row = cell[0] + dir[0];
                int col = cell[1] + dir[1];
                
                //validity check for row and col and if its an obstacle
                if(row < 0 || col < 0 || col >= n || row >= m || rooms[row][col] == -1) continue;
                
                //update distance
                if(rooms[row][col] == Integer.MAX_VALUE){
                    rooms[row][col] = rooms[cell[0]][cell[1]] + 1;
                    queue.add(new int[]{row, col});
                }
            }
        }
    }
}
```
