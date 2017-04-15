Given an unsorted array of integers, find the length of longest increasing subsequence.

For example,
Given [10, 9, 2, 5, 3, 7, 101, 18],
The longest increasing subsequence is [2, 3, 7, 101], therefore the length is 4. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O(n2) complexity.

```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        if(n == 0 || n ==1) return n;
        int[] lis = new int[n];
        
        Arrays.fill(lis, 1);
        for(int i=1;i< n;i++){
            for(int j = 0;j<i;j++){
                if(nums[i] > nums[j] && lis[i] < lis[j] + 1){
                    lis[i] = lis[j] + 1;
                }
            }
        }
        
        int max = lis[0];
       for(int i = 1;i< n ;i++){
           if(lis[i]> max)
            max = lis[i];
       }
       return max;
    }
}

```
