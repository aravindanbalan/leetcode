Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. 
An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. 
You may assume all four edges of the grid are all surrounded by water.

```java
public class Solution {
    int m, n;
    public int numIslands(char[][] grid) {
        if(grid.length == 0) return 0;
        m = grid.length;
        n = grid[0].length;
        
        int islands = 0;
        
        for(int i = 0; i< m ;i++){
            for(int j = 0; j< n ;j++){
                if(grid[i][j] == '1'){
                    //then we have an island
                    ++islands;
                    exploreIsland(grid, i, j);
                }
            }
        }
        
        return islands;
    }
    
    private void exploreIsland(char[][] grid, int i, int j){
        //base case for recursion
        if(i < 0 || j < 0 || i >=m || j >=n || grid[i][j] != '1')
            return;
            
        grid[i][j] = '0'; //process this land
        exploreIsland(grid, i+1, j);
        exploreIsland(grid, i-1, j);
        exploreIsland(grid, i, j+1);
        exploreIsland(grid, i, j-1);
    }
}
```
