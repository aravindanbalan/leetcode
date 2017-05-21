```
Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

For example,
   1
    \
     3
    / \
   2   4
        \
         5
Longest consecutive sequence path is 3-4-5, so return 3.
   2
    \
     3
    / 
   2    
  / 
 1
Longest consecutive sequence path is 2-3,not3-2-1, so return 2.
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
    int max;
    public int longestConsecutive(TreeNode root) {
        if(root == null) return 0;
        
        max = 0;
        longestConsecutiveUtil(root, 0, root.val);
        
        return max;
    }
    
    private void longestConsecutiveUtil(TreeNode root, int curr, int target){
        if(root == null) return;
        
       if(root.val == target) curr++;
       else curr = 1;
       
       max = Math.max(max, curr);
       longestConsecutiveUtil(root.left, curr, root.val+1);
       longestConsecutiveUtil(root.right, curr, root.val+1);
    }
    
}
```
