Given a string, find the length of the longest substring T that contains at most k distinct characters.

For example, Given s = “eceba” and k = 2,

T is "ece" which its length is 3.

//similar to https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/#/description just replace 2 with k
```java
public class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        if(s == null || s.length() == 0 || k==0) return 0;
        int max = 0;
        int end = 0; int begin = 0;
        
        int n = s.length();
        int counter = 0;
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        
        while(end < n){
            char c = s.charAt(end);
            if(map.containsKey(c)){
              map.put(c, map.get(c) +1);   
            }else{
                map.put(c, 1);
            } 
            if(map.get(c) == 1) counter++; //new char
            
            end++;
            //if we have reached a counter of more than 2 then we have 3 distinct characters, so reduce the window so that we have only 2 distinct character
            while(counter > k){
                char beginC = s.charAt(begin);
                if(map.containsKey(beginC)){
                    map.put(beginC, map.get(beginC) -1);
                    if(map.get(beginC) == 0) counter--; //removed character
                }

                begin++;
            }
            max = Math.max(max, end - begin);
        }
        
        return max;

    }
}
```
