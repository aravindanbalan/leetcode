```
Follow up for "Remove Duplicates":
What if duplicates are allowed at most twice?

For example,
Given sorted array nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.
```

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        //1,1 or 1 or [] or 1,2
        if(nums.length <= 2) return nums.length;
        
        int n = nums.length;
        int count = 1;
        int prev = nums[0];
        int index = 1;
        
        for(int i = 1; i< n; i++){
            if(nums[i] == prev && count <2){
                count++;
                nums[index++] = prev;
            }else if(nums[i] != prev){
                count = 1;
                prev = nums[i];
                nums[index++] = nums[i];
            }
        }
        
        return index;
    }
}
```
