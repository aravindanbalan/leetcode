Implement strStr().

Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

```java

public class Solution {
    public int strStr(String haystack, String needle) {
        if(haystack == null || needle == null || needle.length() > haystack.length()) return -1;
        
        //implement a sliding window check
        for(int i = 0; ; i++){
            for(int j = 0; ; j++){
                if(j == needle.length()) return i; //first index is i
                if(i+j == haystack.length()) return -1; // we reached the end of the haystack string and we dont find a substring
                
                if(needle.charAt(j) != haystack.charAt(i+j)) break; //check from next i
            }
        }
    }
}
```
