Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

Example 1:
Input:nums = [1,1,1], k = 2
Output: 2
Note:
The length of the array is in range [1, 20,000].
The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].

```java

//Google question
//Same pattern as https://leetcode.com/problems/continuous-subarray-sum/#/description
//Idea is to store sum till now in hashmap and see if sum - k is already present or not
//value in hashmap for sum key is the number of times it was encountered.

public class Solution {
    public int subarraySum(int[] nums, int k) {
        if(nums.length == 0) return 0;
        
        int result = 0;
        int sum = 0;
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        map.put(0, 1); // since if arr contains k itself and it is a subarray
        
        for(int i = 0; i< nums.length ;i++){
            sum += nums[i];
            
            if(map.containsKey(sum-k)){
                result += map.get(sum-k);  
            }
            
            if(map.containsKey(sum))
                map.put(sum, map.get(sum) +1);
            else
                map.put(sum, 1);
        }
        
        return result;
    }
}
```
