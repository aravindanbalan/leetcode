```
A 2d grid map of m rows and n columns is initially filled with water. We may perform an addLand operation which turns the water at position (row, col) into a land. Given a list of positions to operate, count the number of islands after each addLand operation. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example:

Given m = 3, n = 3, positions = [[0,0], [0,1], [1,2], [2,1]].
Initially, the 2d grid grid is filled with water. (Assume 0 represents water and 1 represents land).

0 0 0
0 0 0
0 0 0
Operation #1: addLand(0, 0) turns the water at grid[0][0] into a land.

1 0 0
0 0 0   Number of islands = 1
0 0 0
Operation #2: addLand(0, 1) turns the water at grid[0][1] into a land.

1 1 0
0 0 0   Number of islands = 1
0 0 0
Operation #3: addLand(1, 2) turns the water at grid[1][2] into a land.

1 1 0
0 0 1   Number of islands = 2
0 0 0
Operation #4: addLand(2, 1) turns the water at grid[2][1] into a land.

1 1 0
0 0 1   Number of islands = 3
0 1 0
We return the result as an array: [1, 1, 2, 3]

Challenge:

Can you do it in time complexity O(k log mn), where k is the length of the positions?
``


```java

public class Solution {
    int[] parent;
    int[] rank;
    int numIslands;
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        if(m == 0 || n == 0)return new ArrayList<Integer>();
        
        int k = positions.length;
        if(k == 0) return new ArrayList<Integer>();
        
        parent = new int[m*n];
        rank = new int[m*n];
        int[][] matrix = new int[m][n];
        
        List<Integer> result = new ArrayList<Integer>();
        
        //set parent to itself
        for(int i = 0; i< m*n ;i++){
           parent[i] = i;
        }
        
        int[][] dirs = {{-1,0}, {1, 0}, {0, 1}, {0, -1}};
        numIslands = 0;
        //for each of the positions in positions
        for(int[] position : positions){
            numIslands++; // increment nums islands and decrement while doing union if necessary
            int pos1 = n * position[0] + position[1];
            matrix[position[0]][position[1]] = 1;
            
            //check all four directions and check if there was an another island nearby and do union
            for(int[] dir : dirs){
                int row = position[0] + dir[0];
                int col = position[1] + dir[1];
                
                //validity check
                if(row < 0 || col< 0 || col>=n || row >= m || matrix[row][col] != 1) continue;
                
                int pos2 = n * row + col;
                union(pos1, pos2);
            }
            
            result.add(numIslands);
        }
        
        return result;
    }
    
    private void union(int node1, int node2){
        //union by rank
        int parent1 = find(node1);
        int parent2 = find(node2);
        
        //important condition, if in same set skip union
        if(parent1 == parent2) return;
        
        //union
        if(rank[parent1] < rank[parent2]){
            parent[parent1] = parent2;
        }else{
            if(rank[parent1] == rank[parent2])
                rank[parent1]++;
            parent[parent2] = parent1;
        }
        
        numIslands--;
    }    
    
    private int find(int node){
        while(parent[node]!=node){
            parent[node] = parent[parent[node]];
            node = parent[node];
        }
        return node;
    }
}
```
