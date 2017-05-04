```
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its zigzag level order traversal as:
[
  [3],
  [20,9],
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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();   
        zigzagLevelOrderUtil(root, 0, result);
        return result;
    }
    
    private void zigzagLevelOrderUtil(TreeNode root, int level, List<List<Integer>> result){
        if(root == null) return;
        
        if(level >= result.size()){
            //add new level list
            result.add(new ArrayList<Integer>());
        }
        
        List<Integer> collection = result.get(level);
        if(level %2 == 0){
            //even level, add at end
            collection.add(root.val);
        }else{
            //odd level , add at first
            collection.add(0, root.val);
        }
        
        //recursion
        zigzagLevelOrderUtil(root.left, level+1, result);
        zigzagLevelOrderUtil(root.right, level+1, result);
    }
}
```
