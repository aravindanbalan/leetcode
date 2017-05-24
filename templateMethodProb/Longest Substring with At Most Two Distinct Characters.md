Given a string, find the length of the longest substring T that contains at most 2 distinct characters.

For example, Given s = “eceba”,

T is "ece" which its length is 3.

```java

public class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        if(s == null || s.length() == 0) return 0;
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
            while(counter > 2){
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

Template
```java
int findSubstring(string s){
        vector<int> map(128,0);
        int counter; // check whether the substring is valid
        int begin=0, end=0; //two pointers, one point to tail and one  head
        int d; //the length of substring

        for() { /* initialize the hash map here */ }

        while(end<s.size()){

            if(map[s[end++]]-- ?){  /* modify counter here */ }

            while(/* counter condition */){ 
                 
                 /* update d here if finding minimum*/

                //increase begin to make it invalid/valid again
                
                if(map[s[begin++]]++ ?){ /*modify counter here*/ }
            }  

            /* update d here if finding maximum*/
        }
        return d;
  }
```
