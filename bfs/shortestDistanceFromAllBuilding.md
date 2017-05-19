```
You want to build a house on an empty land which reaches all buildings in the shortest amount of distance. You can only move up, down, left and right. You are given a 2D grid of values 0, 1 or 2, where:

Each 0 marks an empty land which you can pass by freely.
Each 1 marks a building which you cannot pass through.
Each 2 marks an obstacle which you cannot pass through.
For example, given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2):

1 - 0 - 2 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0
The point (1,2) is an ideal empty land to build a house, as the total travel distance of 3+3+1=7 is minimal. So return 7.
```

```java

public class Solution {
    
    public int shortestDistance(int[][] grid) {
        if(grid.length == 0) return 0;
        
        int m = grid.length;
        int n = grid[0].length;
        
        //DO BFS
        //since it says reachable from all buildings, start with each of the building and do bfs
        int[][] distance = new int[m][n];
        int[][] reach = new int[m][n];
        int numBuildings=0;
        
        for(int i = 0; i< m ;i++){
            for(int j = 0; j< n; j++){
                if(grid[i][j] == 1){ //for each building do bfs
                    numBuildings++;
                    bfs(i, j, distance, reach, grid, m , n);
                }
            }
        }
        
        int minDist = Integer.MAX_VALUE;
        for(int i = 0 ; i < m ; i++){
            for(int j = 0; j< n ;j++){
                //check only for those 0s which are equally reachable from all buildings
                if(grid[i][j] == 0 && reach[i][j] == numBuildings){
                       minDist = Math.min(minDist, distance[i][j]);
                }
            }
        }
        
        return minDist == Integer.MAX_VALUE ? -1 : minDist;
    }
    
    private void bfs(int i , int j , int[][] distance,int[][] reach, int[][] grid, int m , int n){
        //calculate distance of each surrounding empty land from this building
        //for walls donot calculate
                    
        Queue<int[]> queue = new LinkedList<>();
        boolean[][] isVisited = new boolean[m][n];
        queue.offer(new int[]{i, j});
        isVisited[i][j] = true;

        int[][] dirs = {{-1, 0}, {1, 0}, {0, 1}, {0, -1}};
        int level = 1;
        while(!queue.isEmpty()){
            
            //each level contains any of the immediate surrounding 4 cells
            //do for each level because without this for loop, each of immediate nodes will be in next level
            for(int q = 0; q < queue.size(); q++){
                int[] cell = queue.poll();
            
                for(int[] dir : dirs){
                    int row = cell[0] + dir[0];
                    int col = cell[1] + dir[1];
                    
                    //validity check for row and col and obstacle or building check
                    if(row < 0 || col < 0 || col >= n || row >= m || grid[row][col] == 2 || grid[row][col] == 1 || isVisited[row][col]) continue;
                    
                     //The shortest distance from [row][col] to this current building is 'level'
                     //Because distance[row][col] = distance from 1st building + distance from second building + distance from third building and so on
                    distance[row][col] += level;
                    reach[row][col]++; // one more building is reachable from this 0
                    isVisited[row][col] = true;
                     //add to queue
                    queue.offer(new int[]{row, col});
                }
            }
            level++;
        } //BFS complete
    }
}
```
