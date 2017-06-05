```
You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

Example 1:
Input: nums is [1, 1, 1, 1, 1], S is 3. 
Output: 5
Explanation: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```

```java
public class Solution {
    int count = 0;
    public int findTargetSumWays(int[] nums, int S) {
        if(nums.length == 0) return count;
        
        findTargetSumWaysUtil(nums, 0, S, 0);
        return count;
    }
    
    private void findTargetSumWaysUtil(int[] nums, int start, int S, int sum){
        if(start == nums.length && sum == S){
            count++;
            return;
        }
        
        if(start == nums.length) return;
        
        int num = nums[start];
        findTargetSumWaysUtil(nums, start+1, S, sum + num);
        findTargetSumWaysUtil(nums, start+1, S, sum - num);
    }
    
    //solving using DP
    /**
     * The recursive solution is very slow, because its runtime is exponential

    The original problem statement is equivalent to:
    Find a subset of nums that need to be positive, and the rest of them negative, such that the sum is equal to target
    
    Let P be the positive subset and N be the negative subset
    For example:
    Given nums = [1, 2, 3, 4, 5] and target = 3 then one possible solution is +1-2+3-4+5 = 3
    Here positive subset is P = [1, 3, 5] and negative subset is N = [2, 4]
    
    Then let's see how this can be converted to a subset sum problem:
    
                      sum(P) - sum(N) = target
    sum(P) + sum(N) + sum(P) - sum(N) = target + sum(P) + sum(N)
                           2 * sum(P) = target + sum(nums)
    So the original problem has been converted to a subset sum problem as follows:
    Find a subset P of nums such that sum(P) = (target + sum(nums)) / 2
    
    Note that the above formula has proved that target + sum(nums) must be even
     * */
     
    public int findTargetSumWays(int[] nums, int S) {
        if(nums.length == 0) return count;
        
        int sum = 0;
        for(int num : nums) sum += num;
        //as seen above target+sum(nums) needs to be even for getting a solution
        
        return if(sum < S || (sum + S)%2 != 0) ? 0 : findTargetSumWaysUtil(nums, (sum + S)/2);
    }
    
    //same as finding ways of subset which adds up to (sum+S)/2
    private void findTargetSumWaysUtil(int[] nums, int sum){
       int dp[] = new int[sum + 1];
       
       dp[0] = 1; //1 way
       for(int n : nums){
           for(int s = sum; s >= n ; s--){
               dp[s] += dp[s-n]; //total number of ways
           }
       }
       
       return dp[s];
    }
}
```
