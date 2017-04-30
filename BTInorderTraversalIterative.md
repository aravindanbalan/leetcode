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
    public List<Integer> inorderTraversal(TreeNode root) {
        if(root == null){
            return new ArrayList<Integer>();
        }
        
        TreeNode node = root;
        List<Integer> result = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        
        while(node!=null){  //push all left children of root till leaf
            stack.push(node);
            node = node.left;
        }
        
        while(!stack.isEmpty()){
            node = stack.pop();
            result.add(node.val);
            
            if(node.right !=null){
                node = node.right;
                
                //push all left children of this right child till leaf
                while(node!=null){
                    stack.push(node);
                    node = node.left;
                }
            }
        }
        
        return result;
    }
}
```
