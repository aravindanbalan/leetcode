Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters.
No two characters may map to the same character but a character may map to itself.

```java

public class Solution {
    public boolean isIsomorphic(String s, String t) {
        
        if(s == null || t == null)
            return false;
        if(s.length() !=t.length())
            return false;
            
        Map<Character, Character> map = new HashMap<>();
        
        for(int i = 0;i< s.length();i++){
            char a = s.charAt(i);
            char b = t.charAt(i);
            if(map.containsKey(a)){
                if(map.get(a) == b)
                    continue;
                else
                    return false;
            }else{
                if(map.containsValue(b))
                    return false;
                else
                    map.put(a,b);
            }
        }
        
        return true;
    }
}

```
