```
Given a binary search tree with non-negative values, find the minimum absolute difference between values of any two nodes.

Example:

Input:

   1
    \
     3
    /
   2

Output:
1

Explanation:
The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
Note: There are at least two nodes in this BST.
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
    int min;
    Integer prev = null;
    public int getMinimumDifference(TreeNode root) {
        min = Integer.MAX_VALUE;
        minDiffUtil(root);
        return min;
    }
    
    //Inorder applies only if its  a BST
    private void minDiffUtil(TreeNode root){
        if(root == null) return;
        
        //do inorder, since its a BST, if we do inorder we get everything in sorted order. The min diff is achieved if the tree is traversed in sorted order and elements next to each other are the closest.
        minDiffUtil(root.left);
        
        if(prev!=null){
            min = Math.min(min, root.val - prev);
        }
        
        prev = root.val;
        
        minDiffUtil(root.right);
    }
}
```
