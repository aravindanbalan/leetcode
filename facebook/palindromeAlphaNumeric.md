Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.

```java
public class Solution {
    public boolean isPalindrome(String s) {
        if(s == null) return true;
        if(s.length() <= 1) return true;
        
        int start = 0;
        int end = s.length()-1;
        
        while(start < end){
            char st = Character.toLowerCase(s.charAt(start));
            char en = Character.toLowerCase(s.charAt(end));
            
            if((st < 'a' || st > 'z') && (st < '0' || st > '9')){
                start++;
                continue;
            }
            
           if((en < 'a' || en > 'z') && (en < '0' || en > '9')){
                end--;
                continue;
            }
            
            if(st == en){
                start++;
                end--;
            }else{
                return false;
            }
        }
        
        return true;
    }
}
```
