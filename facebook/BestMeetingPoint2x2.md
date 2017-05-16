```
A group of two or more people wants to meet and minimize the total travel distance. You are given a 2D grid of values 0 or 1, where each 1 marks the home of someone in the group. The distance is calculated using Manhattan Distance, where distance(p1, p2) = |p2.x - p1.x| + |p2.y - p1.y|.

For example, given three people living at (0,0), (0,4), and (2,2):

1 - 0 - 0 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0
The point (0,2) is an ideal meeting point, as the total travel distance of 2+2+2=6 is minimal. So return 6.
```


```java
public class Solution {
    public int minTotalDistance(int[][] grid) {
        //its always better to meet at the median of all x points and y points seperately
        if(grid.length == 0 || grid[0].length == 0) return 0;
        
        int m = grid.length;
        int n = grid[0].length;
        List<Integer> xCoord = new ArrayList<Integer>();
        List<Integer> yCoord = new ArrayList<Integer>();
        
        for(int i = 0; i< m ;i++){
            for(int j = 0;j < n ;j++){
                if(grid[i][j] == 1){
                    xCoord.add(i);
                    yCoord.add(j);
                }
            }
        }
        
        return getMin(xCoord) + getMin(yCoord);
    }
    
    private int getMin(List<Integer> coordinates){
        if(coordinates == null || coordinates.size() == 0) return 0;
        
        Collections.sort(coordinates);
        
        int i = 0;
        int j = coordinates.size()-1;
        int count = 0;
        
        while(i < j){
            count += coordinates.get(j--) - coordinates.get(i++);
        }
        return count;
    }
}
```
