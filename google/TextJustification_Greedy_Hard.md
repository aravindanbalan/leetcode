Given an array of words and a length L, format the text such that each line has exactly L characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no extra space is inserted between words.

For example,
words: ["This", "is", "an", "example", "of", "text", "justification."]
L: 16.

```java
public class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        //base cases
        List<String> lines = new ArrayList<String>();
        if(words.length == 0 || maxWidth == 0){
            lines.add("");
            return lines;
        }
        
        /**
         * What we need for each line:
         * 1. get the number of words that fits in L = 16;
         * 2. calculate total length of the words calculated above
         * 3. total length of spaces required in that line
         * 4. equally divide the spaces among the words
         * */
         
         int index = 0;
         int n = words.length;
         
         while(index < n){
             
             int last = index+1;
             int count = words[index].length();
             
             while(last < n && count + words[last].length() + 1 <= maxWidth){
                 count += words[last].length() + 1; //1 for space
                 last++;
             }
             
             StringBuilder sb = new StringBuilder();
             sb.append(words[index]);
             int numWords = last - index -1; // we already included index thats why -1
             int totalSpace = maxWidth - count; // total space required
             
             if(last == n || numWords == 0){
                 //last line - to be left justified
                 for(int i = index+1; i< last ; i++){
                     sb.append(" ");
                     sb.append(words[i]);
                 }
                 
                 //fill rest with spaces
                 for(int i = sb.length() ; i< maxWidth; i++){
                     sb.append(" ");
                 }
                 
             }else{
                 //middle lines case - spaces must be equally split with left most words having more space incase uneven
                 // ask this to the interviewer on how this shud be
                    int space = totalSpace / numWords;
                    int rem = totalSpace % numWords;
                         
                   for(int i = index+1; i< last ; i++){  
                         for(int j = space ; j>0 ;j--){
                             sb.append(" ");
                         }
                         
                         //use to remainder to add extra space for each lefmost word
                         if(rem > 0){
                             sb.append(" ");
                             rem--;
                         }
                         
                         sb.append(" ");
                         sb.append(words[i]);
                   }
             }
             
             lines.add(sb.toString());
             index = last;
         }
         
         return lines;
    }
}
```
