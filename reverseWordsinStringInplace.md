Given an input string, reverse the string word by word. A word is defined as a sequence of non-space characters.

The input string does not contain leading or trailing spaces and the words are always separated by a single space.

For example,
Given s = "the sky is blue",
return "blue is sky the".

Could you do it in-place without allocating extra space?

```java

public class Solution {
    public void reverseWords(char[] s) {
        if(s.length == 0) return;
        
        //reverse the entire char array
        reverse(s, 0, s.length-1);
        
        //reverse each word
        int start = 0;
        for(int i = 0;i < s.length; i++){
            if(s[i] == ' '){
                reverse(s, start, i-1);
                start = i+1;
            }
        }
        
        //reverse last word, if there is only one word
        reverse(s, start, s.length-1);
    }
    
    private void reverse(char[] s, int begin, int end){
        if(begin >= end){
            return;
        }
        
        while(begin < end){
            char temp = s[begin];
            s[begin++] = s[end];
            s[end--] = temp;
        }
    }
}
```
