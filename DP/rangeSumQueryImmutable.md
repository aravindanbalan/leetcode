```
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

Example:
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
Note:
You may assume that the array does not change.
There are many calls to sumRange function.
```

```java
public class NumArray {

    int[] nums;
    int[] sums;
    public NumArray(int[] nums) {
        this.nums = nums;
        int n = nums.length;
        if(n > 0){ 
            sums = new int[n];
        
            //pre compute sums
            sums[0] = nums[0];
            for(int i = 1; i< n;i++){
                sums[i] = sums[i-1] + nums[i];
            }
        }
    }
    
    public int sumRange(int i, int j) {
        if(nums.length == 0) return 0;
        
        if(i == 0 && j >=0){
            return sums[j];
        }
        
        // return sums[j] - sums[i] + nums[i];  we can either do this or substract sums[i-1]
        return sums[j] - sums[i-1];

    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(i,j);
 */
```
