```
You need to construct a string consists of parenthesis and integers from a binary tree with the preorder traversing way.

The null node needs to be represented by empty parenthesis pair "()". And you need to omit all the empty parenthesis pairs that don't affect the one-to-one mapping relationship between the string and the original binary tree.

Example 1:
Input: Binary tree: [1,2,3,4]
       1
     /   \
    2     3
   /    
  4     

Output: "1(2(4))(3)"

Explanation: Originallay it needs to be "1(2(4)())(3()())", 
but you need to omit all the unnecessary empty parenthesis pairs. 
And it will be "1(2(4))(3)".

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
