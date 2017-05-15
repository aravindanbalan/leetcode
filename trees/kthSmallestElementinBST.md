Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note: 
You may assume k is always valid, 1 ? k ? BST's total elements.



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
    // Like Binary search, Idea : count of left tree will give you mid
    public int kthSmallest(TreeNode root, int k) {
        if(root == null) return 0;
        int leftNodeCount = count(root.left); //this is more like number of elements till mid
        
        if(k <= leftNodeCount){
            return kthSmallest(root.left, k);
        }else if(k > leftNodeCount + 1){
            return kthSmallest(root.right, k- leftNodeCount - 1);
        }
        
        return root.val;
    }
    
    private int count(TreeNode root){
        if(root == null) return 0;
        
        return 1 + count(root.left) + count(root.right);
    }
}
```
