Write a function to find the longest common prefix string amongst an array of strings.
```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length ==0) return "";
        
        if(strs.length == 1) return strs[0];
        
        String pre = strs[0];
        
        int i = 1;
        while(i < strs.length){
            //reduce pre such that it is contained in strs[i]
            while(strs[i].indexOf(pre)!=0){
                pre = pre.substring(0, pre.length() -1);
            }
            i++;
        }
        
        return pre;
    }
}
```
