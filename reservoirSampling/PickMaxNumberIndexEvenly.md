https://www.careercup.com/question?id=5669417594650624

```
You have a array with integers:


[ 1, -2, 0, 6, 2, -4, 6, 6 ]
You need to write a function which will evenly return indexes of a max value in the array. 
In the example below max value is 6, and its positions are 3, 6 and 7. So each run function should return random index from the set. 

Try to implement with O(n) for computation and memory. 
Try to reduce memory complexity to O(1).
```
```java
public class Solution {
    int[] nums;
    Random rand;
    int max;
    public Solution(int[] nums) {
        this.nums = nums;
        rand = new Random();
        for(int i = 0; i< nums.length; i++){
          max = Math.max(max, nums[i]);
        }
    }
    
    /**
     * Whento use Reservoir sampling:
     * 1. when the question says array size is large
     * 2. If it says Randomly pick something from a huge list of streams. 
     * */
    public int pick() {
        int result = -1;
        //For any reservoir problem, if asked for random selecting for a target value, then count it and always 
        //do rand(count), so probability is always 1/count
        int count = 0;  //number of target values
        
        for(int i = 0; i< nums.length;i++){
            if(nums[i] != max) continue;
            
            //inc count as we have hit a target value
            count++;
            if(rand.nextInt(count) == 0)
                result = i; //assign i to result
        }
        
        //at the end of the for loop, we would have counted the number of target values and probability of getting a 0 in count is always 1/count
        return result; 
    }
}

```
