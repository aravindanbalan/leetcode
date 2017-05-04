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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
         List<List<Integer>> result = new ArrayList<>();
        levelOrderBottomUtil(root, 0, result);
        return result;
    }
    
    private void levelOrderBottomUtil(TreeNode root, int height, List<List<Integer>> result){
        //base case
        if(root == null) return;
        
        if(height >= result.size()){
            //then we need a new arraylist to be added for storing next level nodes
            result.add(0, new ArrayList<Integer>());
        }
        
        result.get(result.size() - height -1).add(root.val);
        levelOrderBottomUtil(root.left, height+1, result);
        levelOrderBottomUtil(root.right, height+1, result);
    }
}
```
