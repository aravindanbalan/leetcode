```
Given an Android 3x3 key lock screen and two integers m and n, where 1 ≤ m ≤ n ≤ 9, count the total number of unlock patterns of the Android lock screen, which consist of minimum of m keys and maximum n keys.

Rules for a valid pattern:
Each pattern must connect at least m keys and at most n keys.
All the keys must be distinct.
If the line connecting two consecutive keys in the pattern passes through any other keys, the other keys must have previously selected in the pattern. No jumps through non selected key is allowed.
The order of keys used matters.

https://leetcode.com/problems/android-unlock-patterns/#/description
```

```java
public class Solution {
    int[][] skip;
    boolean[] visited;
    int m;
    int n;
    
    public int numberOfPatterns(int m, int n) {
        if(m == 0 || n == 0) return 0;
        if(m == 1 && n==1) return 9; 
        
        this.m = m;
        this.n = n;
        
        skip = new int[10][10];
        visited = new boolean[10];
        
        skip[1][3] = skip[3][1] = 2;
        skip[7][9] = skip[9][7] = 8;
        skip[1][7] = skip[7][1] = 4;
        skip[3][9] = skip[9][3] = 6;
	    skip[1][9] = skip[9][1] = skip[3][7] = skip[7][3] = skip[4][6] = skip[6][4] = skip[2][8] = skip[8][2] = 5;
        
        int count = 0;
        //start from 1 or 3 or 5 or 9 will give you the same number of count. So we can multiply by 4
        //same for 2, 4, 6, 8
        //do once for 5

        //for each of the pattern length m to n
        for(int i = m;i <= n ;i++){
            //i - 1 because 1,2,5 is already chosen in the length
            count += patternUtil(1, i-1) * 4;
            count += patternUtil(2, i-1) * 4;
            count += patternUtil(5, i-1);
        }
        
        return count;
    }
    
    private int patternUtil(int num, int remain){
        if(remain < 0) return 0;
        if(remain == 0) return 1;
        
        int count = 0;
        visited[num] = true;
        
        for(int i = 1; i<= 9; i++){
            //if not visited and adjacent to each other or skipped element is already visited then recurse
            if(!visited[i] && (skip[num][i] == 0 || visited[skip[num][i]])){
                count += patternUtil(i, remain -1);
            }
        }
        
        visited[num] = false;
        return count;
        
    }
}
```
