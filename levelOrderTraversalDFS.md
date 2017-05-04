```
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        //Level order using DFS
        List<List<Integer>> result = new ArrayList<>();
        levelOrderUtil(root, 0, result);
        return result;
    }
    
    private void levelOrderUtil(TreeNode root, int height, List<List<Integer>> result){
        //base case
        if(root == null) return;
        
        if(height >= result.size()){
            //then we need a new arraylist to be added for storing next level nodes
            result.add(new ArrayList<Integer>());
        }
        
        result.get(height).add(root.val);
        levelOrderUtil(root.left, height+1, result);
        levelOrderUtil(root.right, height+1, result);
    }
}
```
