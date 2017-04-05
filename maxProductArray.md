Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.

```java
public class Solution {
    public int maxProduct(int[] nums) {
        int n = nums.length;
        
        if(n == 0){
            return 0;
        }
        if(n==1){
            return nums[0];
        }
        
        int min_end_here = nums[0];
        int max_end_here = nums[0];
        int min_end, max_end;
        int max_so_far = nums[0];
        
        for(int i = 1;i< n;i++){
        //keep track of local maximum and local minimum and find the appropriate max and min by multiplying nums[i]
            max_end = Math.max(Math.max(max_end_here * nums[i], min_end_here * nums[i]), nums[i]);
            min_end = Math.min(Math.min(max_end_here * nums[i], min_end_here * nums[i]), nums[i]);
            max_so_far = Math.max(max_so_far, max_end);
            max_end_here = max_end;
            min_end_here = min_end;
        }
        
        return max_so_far;
    }
}

```
