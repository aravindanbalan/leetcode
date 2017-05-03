Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.

Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

```java
public class Solution {
    private static final String[] LETTERS = new String[]{" ", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<String>();
        if(digits == null || digits.length() == 0){
            return result;
        }
        
        combination(digits, "", 0, result);
        return result;
    }
    
    private void combination(String digits, String prefix, int offset, List<String> result){
        if(offset >= digits.length()){
            result.add(prefix);
            return;
        }
        
        String letters = LETTERS[digits.charAt(offset) - '0'];
        for(int i = 0;i < letters.length(); i++){
            combination(digits, prefix + letters.charAt(i), offset+1, result);
        }
    }
}
```
