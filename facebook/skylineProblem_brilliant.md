```
https://leetcode.com/problems/the-skyline-problem/#/description
```

```java

public class Solution {
    
    class BuildingPoint implements Comparable<BuildingPoint>{
        int x;
        boolean isStart;
        int height;
        
        @Override
        public int compareTo(BuildingPoint o){
            //if x coordinates of these points are not same then place them in ascending order
            if(this.x != o.x){
                return this.x - o.x;
            }else{
                // if its start point then ascending order
                //else if end point then descending order
                
                //if start points overlap then highest height is taken
                //if end points overlap then lowest height is taken
                return (this.isStart ? -this.height : this.height) - (o.isStart ? -o.height : o.height);
            }
        }
    }
    
    public List<int[]> getSkyline(int[][] buildings) {
        
        BuildingPoint[] buildingPoints = new BuildingPoint[buildings.length * 2];
        int index = 0;
        
        for(int[] building : buildings){
            buildingPoints[index] = new BuildingPoint();
            buildingPoints[index].x = building[0];
            buildingPoints[index].isStart = true;
            buildingPoints[index].height = building[2];
            
            buildingPoints[index+1] = new BuildingPoint();
            buildingPoints[index+1].x = building[1];
            buildingPoints[index+1].isStart = false;
            buildingPoints[index+1].height = building[2];
            
            index +=2;
        }
        
        Arrays.sort(buildingPoints);
        //max heap
        PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(Collections.reverseOrder());
        maxHeap.add(0);
        int prevMaxHeight = 0;
        List<int[]> result = new ArrayList<>();
        
        for(BuildingPoint point : buildingPoints){
            
            if(point.isStart){
                //if its start we add height to heap
                maxHeap.add(point.height);
            }else{
                //if its ends then we remove the current point height from heap
                maxHeap.remove(point.height);
            }
            
            int currMaxHeight = maxHeap.peek();
            
            //if it had changed then we have a result to add
            if(prevMaxHeight!=currMaxHeight){
                //add to result
                result.add(new int[]{point.x, currMaxHeight});
                prevMaxHeight = currMaxHeight;
            }
        }
        
        return result;
    }
}
```
