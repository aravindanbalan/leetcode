Given two strings S and T, determine if they are both one edit distance apart.

```java
public class Solution {
    public boolean isOneEditDistance(String s, String t) {
        if(s == null || t == null) return false;
        if(Math.abs(s.length() - t.length()) > 1) return false;
        
        if(s.length() == t.length()) return isOneModify(s,t);
        if(s.length() > t.length()) return isOneDelete(s,t);
        return isOneDelete(t,s);
    }
    
    private boolean isOneModify(String s, String t){
        int count = 0;
        
        for(int i = 0; i< s.length() ; i++){
            if(s.charAt(i) != t.charAt(i)) count++;
        }
        
        return count ==1;
    }
    
    private boolean isOneDelete(String s, String t){
        for(int i = 0, j = 0; i<s.length() && j < t.length(); i++, j++){
            if(s.charAt(i)!= t.charAt(j)){
                return t.substring(j).equals(s.substring(i+1));
            }
        }
        
        return true;
    }
}
```
