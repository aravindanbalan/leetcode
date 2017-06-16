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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder.length == 0 || inorder.length == 0) return null;
        if(preorder.length!= inorder.length) return null;
        
        return buildTreeUtil(0, 0, inorder.length-1, preorder, inorder);
    }
    
    private TreeNode buildTreeUtil(int preStart, int inStart, int inEnd, int[] preorder, int[] inorder){
        if(preStart == preorder.length || inStart > inEnd) return null;
        
        int preRoot = preorder[preStart];
        TreeNode root= new TreeNode(preRoot);
        
        //search preRoot index in inorder array to split into left and right
        int inIndex = 0;
        for(int i = inStart; i<= inEnd; i++){
            if(preRoot == inorder[i]){
                inIndex = i; 
                break;
            }
        }
        
        root.left = buildTreeUtil(preStart + 1, inStart, inIndex - 1, preorder, inorder);
        //preStart + num of nodes between inIndex(root) and left most of the substree in Inorder
        root.right = buildTreeUtil(preStart + (inIndex - inStart) + 1, inIndex + 1, inEnd, preorder, inorder);
        return root;
    }
}
```
