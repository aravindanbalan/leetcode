Given a string which contains only lowercase letters, remove duplicate letters so that every letter appear once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

Example:
Given "bcabc"
Return "abc"

Given "cbacdcbc"
Return "acdb"

```java
public class Solution {
    public String removeDuplicateLetters(String s) {
        //Use a stack and only when the letter is already not visited and lexicographically in order
        
        int[] res = new int[26];
        boolean[] visited = new boolean[26];
        Stack<Character> stack = new Stack();
        
        for(char c : s.toCharArray()){
            res[c-'a']++;
        }
        
        for(char c : s.toCharArray()){
            res[c-'a']--; //character analyzed
            
            //check if already visited
            if(visited[c-'a']) continue;
            
            //before putting onto the stack remove those elements which are not in lexicographical order and still some duplicates left for those in stack then safely remove them and mark them not visited
            while(!stack.isEmpty() && c < stack.peek() && res[stack.peek()-'a']!=0){
                visited[stack.pop() - 'a'] = false;
            }
            
            stack.push(c);
            visited[c-'a'] = true;
        }
        
        StringBuilder sb = new StringBuilder();
        
        while(!stack.isEmpty()){
            sb.insert(0, stack.pop());
        }
        
        return sb.toString();
    }
}
```
