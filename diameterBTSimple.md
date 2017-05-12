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
    int max = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        maxDepth(root);
        return max;
    }
    
       private int maxDepth(TreeNode root) {
        if (root == null) return 0;
        
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        
        max = Math.max(max, left + right);
        
        return Math.max(left, right) + 1;
    }
}
```

```java
//Another method

class Height{
    int height;
}

public class DiameterOfTree {

    public int diameter(Node root){
        Height height = new Height();
        return diameter(root,height);
    }
    
    private int diameter(Node root, Height height){
    
        if(root == null){
            return 0;
        }
        
        Height leftHeight = new Height();
        Height rightHeight = new Height();
        int dial = diameter(root.left,leftHeight);
        int diar = diameter(root.right,rightHeight);
        height.height = Math.max(leftHeight.height, rightHeight.height) + 1;
        return Math.max(Math.max(dial, diar),(1 + leftHeight.height + rightHeight.height));
    }

```
