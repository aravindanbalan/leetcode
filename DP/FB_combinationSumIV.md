Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

Example:

nums = [1, 2, 3]
target = 4

The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

Note that different sequences are counted as different combinations.

Therefore the output is 7.

```java
public class Solution {
    public int combinationSum4(int[] nums, int target) {
        //since all are positive integers, target cannot be zero
        if(nums.length == 0) return 0;
        
        // return combinationSum4Util(nums, target);
         return combinationSum4UtilDP(nums, target);
    }
    
    //this will give TLE when target becomes large, so many stack traces. Use DP
    private int combinationSum4Util(int[] nums, int target){
        if(target == 0){
            return 1; //empty subset
        }
        
        int res = 0;
        for(int i = 0; i< nums.length; i++){
            if(target >= nums[i]){
                res += combinationSum4Util(nums, target - nums[i]);
            }
        }
        return res;
    }
    
    //Bottom up dp solution O(n * target)
    private int combinationSum4UtilDP(int[] nums, int target){
        int[] comb = new int[target+1];
        comb[0] = 1;
        
        for(int i = 1; i<= target; i++){
            for(int j = 0; j<nums.length; j++){
                //if target
                if(i >= nums[j]){
                    comb[i] += comb[i - nums[j]];
                }
            }
        }
        
        return comb[target];
    }
}
```
