Given a non-empty integer array, find the minimum number of moves required to make all array elements equal, where a move is incrementing a selected element by 1 or decrementing a selected element by 1.

You may assume the array's length is at most 10,000.

```java

public class Solution {
    public int minMoves2(int[] nums) {
        //if it can be incremented or decremented by 1 then it means that the number of moves
        //is the difference of each number from its median
        
        //Idea : sort the array
        // then calculate the diff between first and last element and move inwards till mid
        
        if(nums.length == 0) return 0;
        int count = 0;
        int i= 0;
        int j = nums.length-1;
        
        Arrays.sort(nums);
        
        while(i < j){
            count += nums[j]- nums[i];
            i++;
            j--;
        }
        
        return count;
    }
}
```
