```
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

For example, 
Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.


The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. 
In this case, 6 units of rain water (blue section) are being trapped.
```

```java

public class Solution {
    public int trap(int[] height) {
        if(height.length <= 1) return 0;
        
        int leftMax = 0, rightMax = 0, left =0, right = height.length-1;
        int volume = 0;
        
        while(left < right){
            if(height[left] > leftMax){
                leftMax = height[left];
            }
            
            if(height[right] > rightMax){
                rightMax = height[right];
            }
            
            if(leftMax < rightMax){
                //then water is on the left
                volume += leftMax - height[left];
                left++;
            } else{
                volume += rightMax - height[right];
                right--;
            }
        }
        
        return volume;
    }
}
```
