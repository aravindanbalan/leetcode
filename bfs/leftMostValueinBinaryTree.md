```

Given a binary tree, find the leftmost value in the last row of the tree.

Example 1:
Input:

    2
   / \
  1   3

Output:
1
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
    int maxLevel = 0;
    int leftMost = 0;
    public int findBottomLeftValue(TreeNode root) {
        if(root == null) return 0;
        
        findBottomLeftValueUtil(root, 1);
        
        return leftMost;
    }
    
    private void findBottomLeftValueUtil(TreeNode root, int level){
        if(root == null)
            return;
            
        //similar to left side view of a Binary tree
        if(maxLevel < level){
            leftMost = root.val;
            maxLevel = level;
        }
        
        //left tree first
        findBottomLeftValueUtil(root.left, level+1);
        findBottomLeftValueUtil(root.right, level +1);
    }
}
```
