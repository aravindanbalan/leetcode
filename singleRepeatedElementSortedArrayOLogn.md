```
Given a sorted array consisting of only integers where every element appears twice except for one element which appears once. Find this single element that appears only once.

Example 1:
Input: [1,1,2,3,3,4,4,8,8]
Output: 2
Example 2:
Input: [3,3,7,7,10,11,11]
Output: 10
Note: Your solution should run in O(log n) time and O(1) space.
```

```java
public class Solution {
    public int singleNonDuplicate(int[] nums) {
       if(nums.length == 0){
           return -1;
       }
       
       if(nums.length == 1){
           return nums[0];
       }
       
       //we can do a binary search since the array is sorted
        int left = 0;
        int right = nums.length-1;
        
        //Idea is to use the index of the repeating elements
        //if there are 2 3s the first three is always in even index (starting at 0).
        while(left < right){
            
            if(left == right -1){
                //only 2 elements
                if(nums[left] == nums[right-1]){
                    return -1; //no repeating elements
                }
            }
            
            int mid = (left + right)/2;

            if(mid <= right -1 && mid >= left+1 && nums[mid] != nums[mid+1] && nums[mid-1] != nums[mid]){
                return mid; //this is the non-repeating element
            }
            
            if(mid<=right -1 && nums[mid] == nums[mid+1]){
                if(mid %2 != 0)
                    right = mid-1;
                else 
                    left = mid + 2;
            }
            
            else if(mid >= left +1 && nums[mid-1] == nums[mid]){
                if((mid-1) %2 !=0)
                    right = mid-2;
                else 
                    left = mid+1;
            }
        }
        
        return nums[left];
    }
}
```
