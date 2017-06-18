```
Given a non-empty string s and an integer k, rearrange the string such that the same characters are at least distance k from each other.

All input strings are given in lowercase letters. If it is not possible to rearrange the string, return an empty string "".

Example 1:
s = "aabbcc", k = 3

Result: "abcabc"

The same letters are at least distance 3 from each other.
Example 2:
s = "aaabc", k = 3 

Answer: ""

It is not possible to rearrange the string.
Example 3:
s = "aaadbbcc", k = 2

Answer: "abacabcd"

Another possible answer is: "abcabcda"

The same letters are at least distance 2 from each other.
```

```java
public class Solution {
    //O(N) time
    public String rearrangeString(String s, int k) {
        if(s == null || s.length() == 0) return "";
        
        int[] count = new int[26];
        int[] valid = new int[26];
        
        for(char c : s.toCharArray()){
            count[c-'a']++;
        }
        
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i< s.length() ; i++){
            int pos = getValidCharIndexToFill(count, valid, i);  //get a valid char pos form 0 to 26 to fill at index
            if(pos == -1) return "";
            
            count[pos]--;
            valid[pos] = i + k; //next valid position where (char)pos can be filled. Since it needs to be k distance apart
            sb.append((char)('a' + pos));
        }
        
        return sb.toString();
    }
    
    private int getValidCharIndexToFill(int[] count, int[] valid, int index){
        int pos = -1;
        int max = 0;
        
        for(int i = 0; i< 26; i++){
            if(count[i] > 0 && count[i] > max && index >= valid[i]){
                max = count[i];
                pos = i;
            }
        }
        
        return pos;
    }
}
```
