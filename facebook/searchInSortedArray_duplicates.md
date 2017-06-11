```
Follow up for "Search in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Write a function to determine if a given target is in the array.

The array may contain duplicates.
```

```java
public class Solution {
    public boolean search(int[] nums, int target) {
           if(nums.length == 0) return false;
        
        int left = 0, right = nums.length - 1;
        while(left <= right){
            if(nums[left] == target) return true;
            if(nums[right] == target) return true;
                        
            int mid = left + (right - left)/2;
            if(nums[mid] == target) return true;
            
            if(nums[mid] > nums[right]){
                if(target > nums[right] && target < nums[mid])
                    right = mid -1;
                else 
                    left = mid +1;
            }else if(nums[mid] < nums[right]){
                if(target < nums[right] && target > nums[mid])
                    left = mid + 1;
                else 
                    right = mid -1;
            }else{
                right--;
            }
        }
        
        return false;
    }
}
```
