```java
public class Solution {
    public String reverseVowels(String s) {
        if(s == null || s.length() <=1) return s;
        
        Set<Character> set = new HashSet<Character>();
        set.add('a'); set.add('e'); set.add('i'); set.add('o'); set.add('u'); 
        set.add('A'); set.add('E'); set.add('I'); set.add('O'); set.add('U');

        int left = 0, right = s.length() -1;
        char[] str = s.toCharArray();
        
        while(left < right){
            if(set.contains(str[left]) && set.contains(str[right])){
                //swap both characters
                char temp = str[left];
                str[left] = str[right];
                str[right] = temp;
                left++;
                right--;
                continue;
            }
            
            if(!set.contains(str[left])){
                left++;
            }
            
            if(!set.contains(str[right])){
                right--;
            }
        }
        
        return new String(str);
    }
}
```
