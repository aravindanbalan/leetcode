```

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

    1
   / \
  2   2
 / \ / \
3  4 4  3
But the following [1,2,2,null,3,null,3] is not:
    1
   / \
  2   2
   \   \
   3    3
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
    public boolean isSymmetric(TreeNode root) {
        //empty tree
        if(root == null){
            return true;
        }
        
        //leaf nodes
        if(root.left == null && root.right == null){
            return true;
        }
        
        return isSymmetricUtil(root.left , root.right);
    }
    
    private boolean isSymmetricUtil(TreeNode left, TreeNode right){
        if(left == null && right == null){
            return true;
        }
        
        if(left!=null && right == null){
            return false;
        }
        
        if(left== null && right!=null){
            return false;
        }
        
        return (left.val == right.val) && isSymmetricUtil(left.left, right.right) && isSymmetricUtil(left.right , right.left);
    }
}
```
