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
    public String tree2str(TreeNode t) {
        if(t == null) return "";
        String result = Integer.toString(t.val);
        
        String left = tree2str(t.left);
        String right = tree2str(t.right);
        
        //if both empty then single root or leaf node
        if(left == "" && right == "") return result;
        
        //if left is empty then we need an addition () to denote the left null subtree
        if(left == "") return result + "()" + "(" + right + ")";
        
        //if right is empty then we dont need an addition () to denote the right null subtree
        if(right == "") return result + "(" + left + ")";
        
        return result + "(" + left + ")" + "(" + right + ")";
    }
}
```
