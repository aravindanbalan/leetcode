Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

For example,
S = "ADOBECODEBANC"
T = "ABC"
Minimum window is "BANC".



```
Using the same template like for finding all anagrams
There is an awesome template for all these problems 

https://leetcode.com/problems/find-all-anagrams-in-a-string/#/solutions
https://discuss.leetcode.com/topic/30941/here-is-a-10-line-template-that-can-solve-most-substring-problems
```

```java
public class Solution {
    public String minWindow(String s, String t) {
        if(s == null || s.length() == 0 || t == null || t.length() == 0 || t.length() > s.length()){
            return "";
        }
        
        int counter;
        int begin = 0, end = 0; //sliding window pointers
        int head = 0;
        int len = Integer.MAX_VALUE; // since we are finding the minimum window
        Map<Character, Integer> map = new HashMap<Character, Integer>(); //will store the count of each character
        
        for(char c : t.toCharArray()){
            if(map.containsKey(c)){
                map.put(c, map.get(c) + 1);
            }else{
                map.put(c, 1);
            }
        }
        
        counter = map.size();
        
        while(end < s.length()){
            
            char c = s.charAt(end);
            if(map.containsKey(c)){
                map.put(c, map.get(c) -1); //decrement map value as we have encountered a character in map
                if(map.get(c) == 0) counter--;
            }
            
            end++;
            
            while(counter == 0){ //then we have encountered all the characters we want in t
                //update min length value
                if(len > (end - begin)){
                    head = begin;
                    len = end - begin;
                }
                
                //move the sliding window now
                char tempc = s.charAt(begin);
                if(map.containsKey(tempc)){
                    map.put(tempc, map.get(tempc) +1);
                    if(map.get(tempc) > 0 ) counter++;
                }
                begin++;
            }
        }
        
        if(len == Integer.MAX_VALUE) return "";
        return s.substring(head, head+len);
    }
}
```
