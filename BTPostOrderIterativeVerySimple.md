
``` 
Brilliant solution : http://www.programcreek.com/2012/12/leetcode-solution-of-iterative-binary-tree-postorder-traversal-in-java/
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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        
        //base case
        if(root == null){
            return result;
        }
        
        Stack<TreeNode> stack = new Stack<TreeNode>();
        stack.push(root);
        
        while(!stack.isEmpty()){
            TreeNode temp = stack.peek();  //do not pop
            if(temp.left == null && temp.right == null){
                //this mean we already processed, so pop and add it to list
                TreeNode pop = stack.pop();
                result.add(pop.val);
            }else{
                
                //we need to process its children - right first as its a stack and postorder requires right later and left first to be printed
                
                if(temp.right!=null){
                    stack.push(temp.right);
                    temp.right = null;  // have processed right
                }
                
                 if(temp.left!=null){
                    stack.push(temp.left);
                    temp.left = null;  // have processed left
                }
                
            }
        }
        
        return result;
    }
}
```
