Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]

```java
public class Solution {
    public List<String> generateParenthesis(int n) {
        if(n == 0) return new ArrayList<String>();
        
        List<String> result = new ArrayList<>();
        if(n == 1){
            result.add("()");
            return result;
        }
        
        parenthesisUtil(n, "", 0, 0, result);
        return result;
    }
    
    private void parenthesisUtil(int n, String str, int openCount, int closeCount, List<String> result){
        if(str.length() == 2*n){
            result.add(str);
            return;
        }
        
       if(openCount < n){
           parenthesisUtil(n, str + "(", openCount+1, closeCount, result);
       }
       
       //so we have recursively added openCount ( . now time to add equal ) parenthesis.
       if(closeCount < openCount){
           parenthesisUtil(n, str + ")", openCount, closeCount +1, result);
       }
    }
}
```
