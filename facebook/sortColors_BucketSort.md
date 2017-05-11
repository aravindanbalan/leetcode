Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

```java
public class Solution {
    public void sortColors(int[] nums) {
        //no need to sort
        if(nums.length <=1) return;
        int numColors = 3;
        
        //we can use bucket sort
        int[] buckets = new int[numColors];
        
        for(int i=0;i<nums.length;i++){
            buckets[nums[i]]++;
        }
        
        int j = 0;
        for(int i = 0;i < numColors;i++){
            int n = buckets[i];
            if(n > 0){
               while(j< nums.length && n > 0){
                 nums[j++] = i;
                 n--;
               } 
            }
        }
        
    }
}
```
