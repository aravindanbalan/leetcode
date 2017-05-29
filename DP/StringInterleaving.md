Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

For example,
Given:
s1 = "aabcc",
s2 = "dbbca",

When s3 = "aadbbcbcac", return true.
When s3 = "aadbbbaccc", return false.

```java
public class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        
        int l1 = s1.length();
        int l2 = s2.length();
        int l3 = s3.length();
        
        if(l3 != l1 + l2) return false;
        
        boolean table[][] = new boolean[l1+1][l2+1];
        table[0][0] = true; //both empty strings
        
        //if s2 is empty
        for(int i = 1; i<= l1;i++){
            table[i][0] = table[i-1][0] && s1.charAt(i-1) == s3.charAt(i-1);
        }
        
        //if s1 is empty
        for(int j = 1; j<= l2;j++){
            table[0][j] = table[0][j-1] && s2.charAt(j-1) == s3.charAt(j-1);
        }
        
        for(int i = 1; i<=l1; i++){
            for(int j = 1; j<=l2; j++){
            
            table[i][j] = (table[i-1][j] && s1.charAt(i-1) == s3.charAt(i+j-1)) 
                  || (table[i][j-1] && s2.charAt(j-1) == s3.charAt(i+j-1) );
            }
        }
        
        return table[l1][l2];
    }
}
```
