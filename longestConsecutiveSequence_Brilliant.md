```
Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,
Given [100, 4, 200, 1, 3, 2],
The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.

Your algorithm should run in O(n) complexity.
```

```java

public class Solution {
    public int longestConsecutive(int[] nums) {
        if(nums.length == 0) return 0;
        
        int n = nums.length;
        int max = 0;
        //store all nums in index
        Set<Integer> set = new HashSet<Integer>();
        for(int num : nums){
            set.add(num);
        }
    
        for(int num : nums){
            if(set.contains(num)){
                int val = num;
                int count = 1;
                
                //reduce all consecutive val lesser than val.
                while(set.remove(val-1)) val--; 
                count += num - val;
                
                //reset val
                val = num;
                
                //reduce all consecutive val greater than val.
                while(set.remove(val+1)) val++; 
                count += val - num;
                
                max = Math.max(max, count);
            }
            
            //if its not in set then it would have been processed already
        }
        
        return max;
    }
}
```
