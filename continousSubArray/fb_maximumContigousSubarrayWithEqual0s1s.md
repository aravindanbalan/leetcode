
```
Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

Example 1:
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
Example 2:
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

```java
public class Solution {
    public int findMaxLength(int[] nums) {
    
        if(nums.length < 2) return 0;
        //Idea is to convert all zeros to -1 then process
    
        //convert the original array
        for(int i = 0; i< nums.length ; i++){
            if(nums[i] == 0) nums[i] = -1;
        }    
        
        //now if we find the sum till i and if its zero then we have equal number of 1s and 0s.
        //we store that sum till i each time and fetch the last index found to maximize
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        map.put(0, -1); //put sum 0 at index -1 for case [0,1] we need 2
        
        int sum = 0;
        int max = 0;
        
        for(int i = 0; i< nums.length ; i++){
            sum += nums[i];
            
            if(map.containsKey(sum)){
                max = Math.max(max, i - map.get(sum)); //update max
            }else{
                map.put(sum, i); //store sum till now with index i
            }
        }
        
        return max;
    }
}
```
