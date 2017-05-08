You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

```java
public class Solution {
    public int climbStairs(int n) {
        if(n<=0) return 0;
        if(n == 1) return 1;
        if(n==2) return 2;
        
        int[] climb = new int[n+1];
        climb[0] = 0;
        climb[1] = 1;
        climb[2] = 2;
        
        for(int i = 3; i<= n;i++){
            climb[i] = climb[i-1] + climb[i-2];
        }
        
        return climb[n];
    }
}
```
