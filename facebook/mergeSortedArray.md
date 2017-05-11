```java
public class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        if(n==0) return;
      
        
        int first = m-1;
        int second = n-1;
        int k = m+n-1;
        
        while(first >=0 && second >= 0){
            if(nums1[first] > nums2[second]){
                nums1[k--] = nums1[first--];
            }else{
                nums1[k--] = nums2[second--];
            }
        }
        
        while(first >= 0)
            nums1[k--] = nums1[first--];
        
        while(second >= 0)
            nums1[k--] = nums2[second--];
    }
}
```
