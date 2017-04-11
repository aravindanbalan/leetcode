```
Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

For example:
Given the following binary tree,
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
You should return [1, 3, 4].

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
    List<Integer> result;
    int maxLevel;
    public List<Integer> rightSideView(TreeNode root) {
        result = new ArrayList<>();
        if(root == null) return result;
        
        rightSideViewUtil(root, result, 1);
        return result;
    }
    
    private void rightSideViewUtil(TreeNode root, List<Integer> result, int level){
        if(root == null) {
            return;
        }
        
        if(maxLevel < level){
            result.add(root.val);
            //print one for the level. since we go to right first left gets ignored if printed
            maxLevel = level;
        }
        rightSideViewUtil(root.right, result, level + 1);
        rightSideViewUtil(root.left, result, level + 1);
    }
}
```
