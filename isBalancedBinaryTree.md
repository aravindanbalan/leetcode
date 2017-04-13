Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

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
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
       
       int leftHeight = depth(root.left);
       int rightHeight = depth(root.right);
       
       return Math.abs(leftHeight - rightHeight) <=1 && isBalanced(root.left) && isBalanced(root.right);
    }
    
    private int depth(TreeNode root){
        if(root == null) return 0;
        
        return Math.max(depth(root.left), depth(root.right)) + 1;
        
    }
}

```
Below is best as the above one traverses each node more than once.

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
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
        
       return isBalancedUtil(root)!=-1;
    }
    
    private int isBalancedUtil(TreeNode root){
        if(root == null) return 0;
        
        int left = isBalancedUtil(root.left);
        if(left == -1) return -1; //left subtree is un-balanced.
        int right = isBalancedUtil(root.right);
        if(right == -1) return -1;
        
        if(Math.abs(left - right) > 1) return -1;
        
        return Math.max(left, right) + 1;
    }
}
```

