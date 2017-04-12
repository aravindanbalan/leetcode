Given a binary tree, return the values of its boundary in anti-clockwise direction starting from root.
Boundary includes left boundary, leaves, and right boundary in order without duplicate nodes.

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
    List<Integer> result;
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        if(root == null) return new ArrayList<>();
        
        result = new ArrayList<>();
        boundaryUtil(root, result);
        return result;
    }
    
    private void boundaryUtil(TreeNode root, List<Integer> result){
        result.add(root.val);
        addLeftBoundary(root.left, result);
        addLeafBoundary(root.left, result);
        addLeafBoundary(root.right, result);
        addRightBoundary(root.right,result);
    }
    
    private void addLeftBoundary(TreeNode root, List<Integer> result){
        if(root == null) return;
        
        //non leaf node check as leaf nodes will be covered by next function
        if(root.left!=null || root.right!=null) result.add(root.val);
        
        if(root.left == null){
            addLeftBoundary(root.right, result);
        }else {
            addLeftBoundary(root.left, result);
        }
    }
    
    private void addLeafBoundary(TreeNode root, List<Integer> result){
        if(root == null) return;
        
        if(root.left == null && root.right == null) {
            result.add(root.val);
            return;
        }
        addLeafBoundary(root.left, result);
        addLeafBoundary(root.right, result);
    }
    
    private void addRightBoundary(TreeNode root, List<Integer> result){
        if(root == null) return;
        
        if(root.right == null){
            addRightBoundary(root.left, result);
        }else {
            addRightBoundary(root.right, result);
        }
        if(root.left!=null || root.right!=null) result.add(root.val);
    }
}

```
