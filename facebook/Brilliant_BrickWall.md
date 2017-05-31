```
https://leetcode.com/problems/brick-wall/#/description

There is a brick wall in front of you. The wall is rectangular and has several rows of bricks. The bricks have the same height but different width. You want to draw a vertical line from the top to the bottom and cross the least bricks.

The brick wall is represented by a list of rows. Each row is a list of integers representing the width of each brick in this row from left to right.

If your line go through the edge of a brick, then the brick is not considered as crossed. You need to find out how to draw the line to cross the least bricks and return the number of crossed bricks.

You cannot draw a line just along one of the two vertical edges of the wall, in which case the line will obviously cross no bricks.

Example:
Input: 
[[1,2,2,1],
 [3,1,2],
 [1,3,2],
 [2,4],
 [3,1,2],
 [1,3,1,1]]
Output: 2
```

```java

public class Solution {
    public int leastBricks(List<List<Integer>> wall) {
        if(wall.size() == 0) return 0;
        
        
        /**
         * Idea is as follows:
         * 
         * 1. View each row as vertex and each total length of (0...i) as edges coming out of the vertex
         * 
         * 2. first vertex (row 0) will have edges e1 = 1, e2= 3, e3 = 5, e4 = 6
         *      second vertex(row 1) will have edges e1 = 3, e2=4, e3 = 6 etc.
         * 
         * 3. We count the number of occurences of each edge length and store it.
         * 
         * 4. If we see carefully, we need to cut in a place after the maximum occuring edge which is 4 here so that we minimize the number of bricks which are crossing the vertical line.
         * 
         * 5. So find the maximum occuring edge count and substract it from wall.size() to get the number of bricks crossing.
         * */
        
        int count = 0;
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        
        for(List<Integer> list : wall){
            int length = 0;
            
            for(int i = 0; i< list.size() -1 ; i++){
                length += list.get(i);
                
                //count the edge lengths
                if(map.containsKey(length)){
                    map.put(length , map.get(length) +1);
                }else{
                    map.put(length, 1);
                }
                
                //update count to find the maximum edge
                count = Math.max(count, map.get(length));
            }
        }
        
        //return number of bricks crossing
        return wall.size() - count;
    }
}
```
