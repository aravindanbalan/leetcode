```
There are a row of n houses, each house can be painted with one of the k colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a n x k cost matrix. For example, costs[0][0] is the cost of painting house 0 with color 0; costs[1][2] is the cost of painting house 1 with color 2, and so on... Find the minimum cost to paint all houses.

Note:
All costs are positive integers.

Follow up:
Could you solve it in O(nk) runtime?
```

```java
public class Solution {
    public int minCostII(int[][] costs) {
        if(costs.length == 0 || costs[0].length == 0) return 0;
        
        int n = costs.length;
        int k = costs[0].length;
        
        //only one color, check if there is only 1 house or not
        if(k==1) return n==1 ? costs[0][0]: -1;
        
        //int[][] dp = new int[n][k];
        //The formula will be dp[i][j] = Math.min(any k!= j| dp[i-1][k]) + costs[i][j].
        //But the above will take O(n * k^2)
        //we need a loop for each house and a loop for each j and loop for each k and k!=j

        //So here all we need to know is the previous min and second min and the paint chosen for house i while painting i+1.
        //if min was chosen and j was the paint, then choose second min from previous to paint current one.
        //This will reduce the complexity to O(nk).
        
        int prevPaintInd = -1; int prevMin = 0, prevSecondMin = 0;
        
        //for each house
        for(int i = 0; i< n ; i++){
            //these will store the local min and second min and the paint chosen
            int paintInd = -1, min = Integer.MAX_VALUE, secondMin = Integer.MAX_VALUE;
            
            for(int j = 0; j< k; j++){
                //if current index is equal to previously chosen paint then use second min or first min
                int val = costs[i][j] + (j == prevPaintInd ? prevSecondMin : prevMin);
                
                //update local values accordingly.
                if(paintInd == -1){
                    paintInd = j;
                    min = val;
                }else if(val < min){
                    secondMin = min; //secondMin becomes previous min
                    min = val;
                    paintInd = j;
                }else if(val < secondMin){
                    //if min <= val < secondMin 
                    secondMin = val;
                }
            }
            
            //update the previous values as we are gonna paint the next house
            prevPaintInd = paintInd;
            prevMin = min;
            prevSecondMin = secondMin;
        }
        
        return prevMin;
    }
}
```
