
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:
Given the below binary tree and sum = 22,

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
    public boolean hasPathSum(TreeNode root, int sum) {
     
     if(root == null){
        return false;
     }   
     
     //leaf node check
     if(root.val == sum && root.left == null && root.right == null) return true;
     
     return (hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val));
     
    }
}
```
