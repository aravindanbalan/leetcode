```

Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

Note:
You must not modify the array (assume the array is read only).
You must use only constant, O(1) extra space.
Your runtime complexity should be less than O(n2).
There is only one duplicate number in the array, but it could be repeated more than once.
```

```java
public class Solution {
//This will work only if the array values are from 1...n
    public int findDuplicate(int[] nums) {
        if(nums.length == 0) return -1;
        
        int slow = nums[0];
        int fast = nums[nums[0]];
        
        //Idea : like linked list cycle 2 where we need to find the start of the cycle
        
        //this will end if there is a cycle(duplicate), slow will be inside the loop
        while(fast != slow){
            fast = nums[nums[fast]];
            slow = nums[slow];
        }
        
        fast = 0;
        while(fast!=slow){
            fast = nums[fast];
            slow = nums[slow];
        }
        
        return slow;
    }
}
```
