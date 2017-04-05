Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.


```java
public class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        
        if(n==0)
            return 0;
        if(n ==1)
            return nums[0];
            
        int max_so_far = nums[0];
        int max_end_here = nums[0];
        
        for(int i = 1;i<n ;i++){
            max_end_here = Math.max(nums[i], nums[i] + max_end_here);
            max_so_far = Math.max(max_so_far, max_end_here);
        }
        
        return max_so_far;
    }
}
```
