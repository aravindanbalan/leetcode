```

Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.
Example 1: 
Input:

0 0 0
0 1 0
0 0 0
Output:
0 0 0
0 1 0
0 0 0
```

```java

public class Solution {
    public int[][] updateMatrix(int[][] matrix) {
     //Do BFS
     
     //Preprocess, set Integer.MAX_VALUE for all 1s and others add to queue
     
     int m = matrix.length;
     int n = matrix[0].length;
     
     Queue<int[]> queue = new LinkedList();
     for(int i = 0;i < m ;i++){
         for(int j = 0;j < n ; j++){
             
             //if it is 1 then it needs to be updated with the min distance
             if(matrix[i][j] == 1){
                 matrix[i][j] = Integer.MAX_VALUE;
             }else{
                 //add to queue
                 queue.add(new int[]{i, j});
             }
         }
     }
     
     //all four directions
     int[][] directions = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
     
    while(!queue.isEmpty()){
        int[] cell = queue.poll();
        
        //check for all four directions
        for(int[] dir : directions){
            int row = cell[0] + dir[0];
            int col = cell[1] + dir[1];
            
            // new row, col is less than current cell[0] and cell[1] + 1
            if(row < 0 || row >= m || col < 0 || col >=n ||
            matrix[row][col] <= matrix[cell[0]][cell[1]] +1) 
                continue;
                
            queue.add(new int[]{row, col});
            matrix[row][col] = matrix[cell[0]][cell[1]] +1; //compute distance.
        }
    }
    
    return matrix;
     
    }
}
```
