```
Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:
Return true if there exists i, j, k 
such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 else return false.
Your algorithm should run in O(n) time complexity and O(1) space complexity.
```

```java

public class Solution {
    public boolean increasingTriplet(int[] nums) {
        //keep track of small and next small numbers till now
        int small = Integer.MAX_VALUE, big = Integer.MAX_VALUE;
        
        for(int num : nums){
            if(num <= small)
                small = num;
            else if(num <= big) //second small num
                big = num;
            else //we have found our third small number in increasing order
                return true;
        }
        
        return false;
    }
}
```
