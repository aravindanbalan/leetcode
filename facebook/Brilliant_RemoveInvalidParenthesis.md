```
Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.

Note: The input string may contain letters other than the parentheses ( and ).

Examples:
"()())()" -> ["()()()", "(())()"]
"(a)())()" -> ["(a)()()", "(a())()"]
")(" -> [""]

```

```java

public class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> result = new ArrayList<String>();
        if(s == null || s.length() == 0){
          result.add("");
          return result;
        } 

        //Idea is to do BFS and remove either ) or ( and do bfs on the next new string. At each level we eliminate a ( or ) and check for its validity, if ok add to result
        Queue<String> queue = new LinkedList<String>();
        
        Set<String> visited = new HashSet<String>();
        
        queue.add(s);
        visited.add(s);
        
        boolean found = false;
        
        while(!queue.isEmpty()){
            String str = queue.poll();
            
            if(isValid(str)){
                result.add(str); //add it to result
                found = true; 
            }
            
            if(found) continue; //continue with other strings even if invalid since we have found the end goal in this level
            
            for(int i = 0; i< str.length() ; i++){
                //remove either ) or ( at each each index i
                if(str.charAt(i)!=')' && str.charAt(i) != '(') continue; //remove only parenthesis
                
                String t = str.substring(0, i) + str.substring(i+1); //new string after removing character at i 
                
                //not visited already - for case str = "())" , removing any of the ) will give the same string again
                if(!visited.contains(t)){
                    queue.add(t);
                    visited.add(t);
                }
            }
        }
        
        return result;
    }
    
    private boolean isValid(String str){
        int count = 0;
        
        //s = ()())( is false since its not valid as its end up with )(
        for(int i = 0; i< str.length() ; i++){
            if(str.charAt(i) == ')' && count == 0) return false;
            if(str.charAt(i) == ')') count--;
            if(str.charAt(i) == '(') count++;
        }
        
        return count==0;
    }
}
```
