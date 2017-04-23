Given an absolute path for a file (Unix-style), simplify it.

For example,
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"
click to show corner cases.

Corner Cases:
Did you consider the case where path = "/../"?
In this case, you should return "/".
Another corner case is the path might contain multiple slashes '/' together, such as "/home//foo/".
In this case, you should ignore redundant slashes and return "/home/foo".


```java
public class Solution {
    public String simplifyPath(String path) {
        if(path == null || path.isEmpty()) return "/";
        Stack<String> stack = new Stack<String>();
        Set<String> skip = new HashSet<String>(Arrays.asList(".", "", ".."));
        
        for(String dir : path.split("/")){
            if(dir.equals("..") && !stack.isEmpty()) stack.pop();
            else if(!skip.contains(dir)) stack.push(dir);
        }
        
        String res = "";
        for(String dir : stack) res += "/" + dir;
        
        return res.isEmpty() ? "/" : res; 
    }
}
```
