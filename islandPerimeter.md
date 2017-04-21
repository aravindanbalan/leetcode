You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water. 
Grid cells are connected horizontally/vertically (not diagonally). 
The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells). 
The island doesn't have "lakes" (water inside that isn't connected to the water around the island). 
One cell is a square with side length 1. 
The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

```java
public class Solution {
    public int islandPerimeter(int[][] grid) {
        int islands = 0;
        int neighbors = 0;
        //Other way of doing it -- see comment code
        //int result= 0;
        
        for(int i = 0;i< grid.length;i++){
            for(int j=0;j< grid[0].length;j++){
                if(grid[i][j] == 1){
                    ++islands;
                    //result +=4;
                    
                    if(i<grid.length-1 && grid[i+1][j] == 1) ++neighbors;
                    if(j<grid[0].length -1 && grid[i][j+1] == 1) ++neighbors;
                    
                    //  if(i<grid.length-1 && grid[i+1][j] == 1) result -=2;
                    // if(j<grid[0].length -1 && grid[i][j+1] == 1) result -=2;
                }
            }
        }
        
        //return result;
        return 4*islands - 2*neighbors;
    }
}

```
