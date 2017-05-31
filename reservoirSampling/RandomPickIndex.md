```
Given an array of integers with possible duplicates, randomly output the index of a given target number. You can assume that the given target number must exist in the array.

Note:
The array size can be very large. Solution that uses too much extra space will not pass the judge.

Example:

int[] nums = new int[] {1,2,3,3,3};
Solution solution = new Solution(nums);

// pick(3) should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
solution.pick(3);

// pick(1) should return 0. Since in the array only nums[0] is equal to 1.
solution.pick(1);
```

```java
public class Solution {
    int[] nums;
    Random rand;
    
    public Solution(int[] nums) {
        this.nums = nums;
        rand = new Random();
    }
    
    /**
     * Whento use Reservoir sampling:
     * 1. when the question says array size is large
     * 2. If it says Randomly pick something from a huge list of streams. 
     * */
    public int pick(int target) {
        int result = -1;
        //For any reservoir problem, if asked for random selecting for a target value, then count it and always 
        //do rand(count), so probability is always 1/count
        int count = 0;  //number of target values
        
        for(int i = 0; i< nums.length;i++){
            if(nums[i] != target) continue;
            
            //inc count as we have hit a target value
            count++;
            if(rand.nextInt(count) == 0)
                result = i; //assign i to result
        }
        
        //at the end of the for loop, we would have counted the number of target values and probability of getting a 0 in count is always 1/count
        return result; 
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int param_1 = obj.pick(target);
 */
```
