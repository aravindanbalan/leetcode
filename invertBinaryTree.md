
```
Invert a binary tree.

     4
   /   \
  2     7
 / \   / \
1   3 6   9
to
     4
   /   \
  7     2
 / \   / \
9   6 3   1

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
    TreeNode newRoot;
    public TreeNode invertTree(TreeNode root) {
        if(root == null){
            return root;
        }
        newRoot = root;
        invertTreeUtil(newRoot);
        return newRoot;
    }
    
    private void invertTreeUtil(TreeNode root){
        if(root == null){
            return;
        }
        
        if(root.left == null && root.right == null){
            return; //leaf node;
        }
        
        TreeNode temp = root.right;
        root.right = root.left;
        root.left = temp;
        
        invertTreeUtil(root.left);
        invertTreeUtil(root.right);
    }
}

```
