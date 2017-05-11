Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

```java
public class Solution {
    public boolean isValid(String s) {
        if(s == null || s.length() == 0) return true;
        
        if(s.length() == 1) return false;
        
        String open = "({[";
        String close = ")}]";
        Stack<Character> stack = new Stack<Character>();
        
        for(char c : s.toCharArray()){
            if(open.indexOf(c) >=0){
                stack.push(c);
            }else if(close.indexOf(c) >=0){
                //match corresponding close bracket
                if(!stack.isEmpty() && stack.peek() == open.charAt(close.indexOf(c))){
                    stack.pop();
                }else{
                    //else push it as there is a mismatch
                    stack.push(c);
                }
            }
        }
        
        return stack.isEmpty();
    }
}
```
