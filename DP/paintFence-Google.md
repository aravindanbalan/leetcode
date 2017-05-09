There is a fence with n posts, each post can be painted with one of the k colors.

You have to paint all the posts such that no more than two adjacent fence posts have the same color.

Return the total number of ways you can paint the fence.

```java
public class Solution {
    public int numWays(int n, int k) {
        if(n==0) return 0; // no way to paint
        if(n==1) return k; // k possible ways of painting one post
        if(n==2) return k* k;
        
        int[] ways = new int[n+1];
        ways[0] = 0;
        ways[1] = k;
        ways[2] = k * k; // both can be painted same color
        
        for(int i=3; i<= n;i++){
            //k ways to paint ith post and k-1 ways to post i-1 , if different color is chosen
            // k ways to paint i & i-1th post of same color and k-1 ways to post i-2th post, if same color is chosen
            // ways[i] = k * (k-1) * ways[i-1] + k * (k-1) * ways[i-2]; 
            ways[i] = (k-1) * (ways[i-1] + ways[i-2]);  
        }
        
        return ways[n];
    }
}
```
