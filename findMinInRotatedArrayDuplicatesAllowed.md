Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

The array may contain duplicates.

```java
public class Solution {
    public int findMin(int[] nums) {
        int n = nums.length;
        
        if(n ==0) return -1;
        if(n==1) return nums[0];
        
        int left = 0;
        int right = n-1;
        
        while(left < right){
            
            if(left == right-1){
                return nums[left]<nums[right]?nums[left]:nums[right];
            }
            
            int mid = (left+right)/2;
            
            if(nums[mid] > nums[mid+1]){
                return nums[mid+1];
            }
            
            if(nums[mid-1] > nums[mid]){
                return nums[mid];
            }
            
            if(nums[mid] > nums[right]){
                //it is on the right
                left = mid+1;
            }else if(nums[mid]< nums[right]){
                right = mid;
            }else{
                //if equal just move the right pointer
                right--;
            }
        }
        
        return -1;
    }
}

```
