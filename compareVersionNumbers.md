```
Compare two version numbers version1 and version2.
If version1 > version2 return 1, if version1 < version2 return -1, otherwise return 0.

You may assume that the version strings are non-empty and contain only digits and the . character.
The . character does not represent a decimal point and is used to separate number sequences.
For instance, 2.5 is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

Here is an example of version numbers ordering:

0.1 < 1.1 < 1.2 < 13.37
```

```java
public class Solution {
    public int compareVersion(String version1, String version2) {
        String s1[] = version1.split("\\.");
        String s2[] = version2.split("\\.");
        
        int n = Math.max(s1.length, s2.length);
        
        for(int i = 0;i< n ; i++){
            int num1 = (i < s1.length) ? Integer.valueOf(s1[i]) : 0;    // get ith section number from version1
            int num2 = (i < s2.length) ? Integer.valueOf(s2[i]) : 0;    //get ith section number from version2 
            
            if(num1 > num2){
                return 1;
            }else if(num1 < num2){
                return -1;
            }
        }
        
        return 0;
    }
}

```
