```
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

Example 1:
     3
    / \
   2   3
    \   \ 
     3   1
Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
Example 2:
     3
    / \
   4   5
  / \   \ 
 1   3   1
Maximum amount of money the thief can rob = 4 + 5 = 9.
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
    public int rob(TreeNode root) {
        return robUtil(root, new HashMap<TreeNode, Integer>());
    }
    
    private int robUtil(TreeNode root, Map<TreeNode, Integer> map){
        if(root == null) return 0;
        
        if(map.containsKey(root))
            return map.get(root);
            
        int val = 0; //will be computed to include root later
        if(root.left!=null){
            val += robUtil(root.left.left, map) + robUtil(root.left.right, map);
        }
        
        if(root.right !=null){
            val += robUtil(root.right.left, map) + robUtil(root.right.right, map);
        }
        
        val = Math.max(val + root.val, robUtil(root.left, map) + robUtil(root.right, map));
        map.put(root, val);
        
        return val;
    }
}
```
