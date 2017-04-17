
```
Given a binary tree, return all root-to-leaf paths.

For example, given the following binary tree:

   1
 /   \
2     3
 \
  5
All root-to-leaf paths are:

["1->2->5", "1->3"]

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
    List<String> result;
    public List<String> binaryTreePaths(TreeNode root) {
        if(root == null){
            return new ArrayList<String>();
        }
        
        result = new ArrayList<>();
        binaryTreePathUtil(root , "");
        return result;
    }
    
    private void binaryTreePathUtil(TreeNode root, String path){
        if(root == null){
            return;
        }
        
        path += root.val+"->";
        if(root.left == null && root.right == null){
            result.add(path.substring(0, path.lastIndexOf("->")));
            return;
        }
        
        binaryTreePathUtil(root.left, path);
        binaryTreePathUtil(root.right, path);
    }
}
```
