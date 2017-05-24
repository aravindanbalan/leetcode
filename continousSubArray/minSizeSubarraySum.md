Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.

For example, given the array [2,3,1,2,4,3] and s = 7,
the subarray [4,3] has the minimal length under the problem constraint.

```java
public class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if(nums.length == 0 || s == 0){
            return 0;
        }
        
        int begin = 0;
        int end = 0;
        int minLen = Integer.MAX_VALUE;
        
        int sum = 0;
        while(end < nums.length){
            sum += nums[end];
            
            //if sum has exceeded the given value of s
            if(sum >= s){
                //try to advance begin such that the sum again comes close to s
                while((sum-nums[begin]) >= s){
                    sum -= nums[begin];
                    begin++;
                }
                
                //update min length
                if(minLen > (end - begin +1)){
                    minLen = (end - begin +1);
                }
            }
            
            end++;
        }
        
        if(minLen == Integer.MAX_VALUE) return 0;
        return minLen;
    }
}
```
