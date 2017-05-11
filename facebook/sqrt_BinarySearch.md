```java
public class Solution {
    public int mySqrt(int x) {
        // if(x <= 0) return x;
        // if(x == 1) return 1;
        
        // int k = 0;
        // int j = 1;
        // int root = 0;
        // while((k+j) <= x){
        //     k = k+j;
        //     j +=2;
        //     root++;
        // }
        
        // return root;
        
        //use binary search
        
        int left = 1; int right = x;
        int ans = 0;
        while(left <= right){
            int mid = left + (right-left)/2;  // use always left+ (right-left)/2 to avoid integer overflow

            if(mid <= x/mid){
                left = mid+1;
                ans = mid;
            }else {
                right = mid-1;
            }
        }
        
        return ans;
    }
}
```
