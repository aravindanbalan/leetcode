Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

Note: If the given node has no in-order successor in the tree, return null.

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
    //Iterative - O(n) - doesnt scale if its huge tree
    // public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
    //     if(root == null || p == null) return null;
        
    //     List<TreeNode> inorderList = new ArrayList<TreeNode>();
    //     inOrderUtil(root, inorderList);
        
    //     for(int i = 0; i< inorderList.size(); i++){
    //         if(inorderList.get(i).val == p.val){
    //             if(i == inorderList.size() - 1) return null;
    //             return inorderList.get(i+1);
    //         }
    //     }
        
    //     return null;
    // }
    
    // private void inOrderUtil(TreeNode root, List<TreeNode> inorderList){
    //     if(root == null) return;
        
    //     inOrderUtil(root.left, inorderList);
    //     inorderList.add(root);
    //     inOrderUtil(root.right, inorderList);
    // }
    
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if(root == null) return null;
        
        if(root.val <= p.val){
            return inorderSuccessor(root.right, p);
        }else{
            TreeNode left = inorderSuccessor(root.left, p);
            return (left!=null) ? left : root;
        }
    }
    
     public TreeNode inorderPredecessor(TreeNode root, TreeNode p) {
        if(root == null) return null;
        
        if(root.val >= p.val){
            return inorderPredecessor(root.left, p);
        }else{
            TreeNode right = inorderPredecessor(root.right, p);
            return (right!=null) ? right : root;
        }
    }
    
}
```
