```
You have n super washing machines on a line. Initially, each washing machine has some dresses or is empty.

For each move, you could choose any m (1 ≤ m ≤ n) washing machines, and pass one dress of each washing machine to one of its adjacent washing machines at the same time .

Given an integer array representing the number of dresses in each washing machine from left to right on the line, you should find the minimum number of moves to make all the washing machines have the same number of dresses. If it is not possible to do it, return -1.

Example1

Input: [1,0,5]

Output: 3

Explanation: 
1st move:    1     0 <-- 5    =>    1     1     4
2nd move:    1 <-- 1 <-- 4    =>    2     1     3    
3rd move:    2     1 <-- 3    =>    2     2     2   
Example2

Input: [0,3,0]

Output: 2

Explanation: 
1st move:    0 <-- 3     0    =>    1     2     0    
2nd move:    1     2 --> 0    =>    1     1     1     
Example3

Input: [0,2,0]

Output: -1

Explanation: 
It's impossible to make all the three washing machines have the same number of dresses. 
```

```java
public class Solution {
    public int findMinMoves(int[] machines) {
        if(machines.length == 0) return -1;
        int sum = 0;
        
        for(int dresses : machines) sum += dresses;
        
        if(sum % machines.length > 0) return -1; //cannot distribute the dresses equally
        
        int avg = sum /machines.length;
        int loss = 0;
        int max  = 0;
        
        //loss array is calculated as number of dress currently there in machine - avg to achieve
        //for [1,0,5,6]  , sum is 12, avg = 3. We need to achive [3,3,3,3]
        //so loss array is [-2,-3,2,3] (dresses - avg)
           
        for(int dresses : machines){
            loss += dresses - avg; // loss value at index 0, 1, 2 ... . Next iteration it is transferred to next that why +=
            
            //abs(loss) means that - that machine requires abs(loss) dresses from the right machines to distribute to its left machines
            //if we take max of of abs(loss) - then we need to perform those many steps anyways to make all equal 
            //update max
            max = Math.max(max, Math.max(Math.abs(loss), dresses - avg)); 
        }
        
        return max;
    }
}
```
