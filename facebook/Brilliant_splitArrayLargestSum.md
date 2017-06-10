```
Given an array which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays. Write an algorithm to minimize the largest sum among these m subarrays.

Note:
If n is the length of array, assume the following constraints are satisfied:

1 ≤ n ≤ 1000
1 ≤ m ≤ min(50, n)
Examples:

Input:
nums = [7,2,5,10,8]
m = 2

Output:
18

Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

```java
public class Solution {
    public int splitArray(int[] nums, int m) {
        if(nums.length == 0) return 0;
        
        int sum = 0;
        int l = Integer.MIN_VALUE;
        for(int num : nums){
            sum += num;
            l = Math.max(num , l);
        }
        
        //if only 1 subarray split then return the entire sum
        if(m==1) return sum;
        
        //Idea is that, the smallest max sum 'l' is the maximum element in the array and largest sum possible 'r' is total sum
        
        int r = sum;
        
        //Greedy method of finding
        //do a binary search and try to do a split for each mid sum
        while(l <= r){
            int mid = l + (r-l)/2;
            if(isValid(nums, m, mid)){
                r = mid -1;
            }else {
                l = mid +1;
            }
        }
        
        return l;
    }
    
    private boolean isValid(int[] nums, int m, int target){
        int total = 0;
        int count = 1; //we already have a split
        
        for(int num : nums){
            total += num;
            //if total exceeded the target, then we need to reset total by num and inc count since we are splitting
            if(total > target){
                count++;
                total = num;
                //check if count > m then we have exceeded the number of splits
                if(count > m) return false;
            }
        }
        
        return true;
    }
}
```
