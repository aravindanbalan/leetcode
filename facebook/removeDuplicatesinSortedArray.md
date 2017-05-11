```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums.length <= 1) return nums.length;
        int newindex = 0;
        int n = nums.length;
        
        for(int i = 1; i< n ;i++){
            if(nums[i] != nums[newindex]){
                newindex++;
                nums[newindex] = nums[i];
            }
        }
        
        return newindex+1;
    }
}
```
