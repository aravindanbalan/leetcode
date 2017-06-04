```
You need to construct a binary tree from a string consisting of parenthesis and integers.

The whole input represents a binary tree. It contains an integer followed by zero, one or two pairs of parenthesis. The integer represents the root's value and a pair of parenthesis contains a child binary tree with the same structure.

You always start to construct the left child node of the parent first if it exists.

Example:
Input: "4(2(3)(1))(6(5))"
Output: return the tree root node representing the following tree:

       4
     /   \
    2     6
   / \   / 
  3   1 5   
Note:
There will only be '(', ')', '-' and '0' ~ '9' in the input string.
An empty tree is represented by "" instead of "()".
```

```java

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode str2tree(String s) {
        if(s == null || s.length() == 0) return null;
        
        int firstLeftParen = s.indexOf("(");
        
        int val = (firstLeftParen == -1)? Integer.parseInt(s) : Integer.parseInt(s.substring(0, firstLeftParen));
        
        TreeNode root = new TreeNode(val);
        if(firstLeftParen == -1) return root;  //no more left parenthesis which means no more children
        
        int start = firstLeftParen; int count = 0;
        
        for(int i = start; i< s.length(); i++){
            if(s.charAt(i) == '(') count ++;
            else if(s.charAt(i) == ')') count --;
            
            if(count == 0 && start == firstLeftParen){ //then we are to process left child recursively
                root.left = str2tree(s.substring(start+1, i));
                start = i+1; //update start so that start != firstLeftParen for right child processing
            }else if(count == 0){  //then process right child recursively
                root.right = str2tree(s.substring(start+1, i));
            }
        }
        
        return root;
    }
}
```
