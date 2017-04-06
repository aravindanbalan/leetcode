Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Solve it without division and in O(n).

For example, given [1,2,3,4], return [24,12,8,6].


```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        
        if(n == 0) return new int[]{};
        if(n ==1) return new int[]{1};
        
        int[] output = new int[n];
        int prod = 1;
        output[n-1] = 1;
        
        for(int i= n -2 ; i>=0;i--){
            output[i] = nums[i+1] * prod;
            prod*=nums[i+1];
        }
        
        prod = 1;
        for(int i=0 ;i< n; i++){
            output[i] *= prod;
            prod *=nums[i];
        }
        
        return output;
    }
}
```
