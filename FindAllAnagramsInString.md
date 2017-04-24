Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.


```
There is an awesome template for all these problems 

https://leetcode.com/problems/find-all-anagrams-in-a-string/#/solutions
https://discuss.leetcode.com/topic/30941/here-is-a-10-line-template-that-can-solve-most-substring-problems

We can solve all these problems with this template
https://leetcode.com/problems/minimum-window-substring/
https://leetcode.com/problems/longest-substring-without-repeating-characters/
https://leetcode.com/problems/substring-with-concatenation-of-all-words/
https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/
https://leetcode.com/problems/find-all-anagrams-in-a-string/

```

```java
public class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        if(p == null || p.length() == 0 || s == null || s.length() == 0 || p.length() > s.length()){
            return new ArrayList<>();
        }
        
        List<Integer> result = new ArrayList<Integer>();
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        
        for(char c : p.toCharArray()){
            if(map.containsKey(c)){
                map.put(c, map.get(c) + 1); //multiple occurences of same char
            }else{
                map.put(c, 1); //first occurence
            }
        }
        
        //sliding window
        int begin = 0;
        int end = 0;
        int counter = map.size(); //should not be p.length() due to repeating characters store in the map as single entry.
        
        while(end < s.length()){
            
            char c = s.charAt(end);
            if(map.containsKey(c)){
                map.put(c, map.get(c)-1);
                if(map.get(c) == 0) counter--;   //only if it becomes zero only then all specific repetitions of c in p is addressed.
            }
            
            end++;
            
            //now move the sliding window to restore the map
            while(counter == 0){
                char tempc = s.charAt(begin);
                if(map.containsKey(tempc)){
                    map.put(tempc, map.get(tempc)+1);
                    if(map.get(tempc) > 0) counter++;
                }
                
                //if end - begin = p.length() and counter == 0 then we have an anagram at begin index
                if(end-begin == p.length()){
                    result.add(begin);
                }
                
                begin++; //begin will slide and move to the next first occurence of any anagram character. 
            }
            
        }
        
        return result;
    }
}

```
