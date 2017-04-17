```
Given a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

Example:

Input: The root of a Binary Search Tree like this:
              5
            /   \
           2     13

Output: The root of a Greater Tree like this:
             18
            /   \
          20     13
Hide Company Tags

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
    TreeNode result;
    List<Integer> valueArray;
    int index;
    public TreeNode convertBST(TreeNode root) {
        if(root == null){
            return root;
        }
        
        if(root.left == null && root.right == null){
            return root;
        }
        
        valueArray = new ArrayList<Integer>();
        preProcessBST(root);
        
        for(int i = valueArray.size()-2;i>=0;i--){
            valueArray.set(i, valueArray.get(i) + valueArray.get(i+1));
        }
        
        index = 0;
        result = root;
        postProcessBST(result, valueArray);
        return result;
    }
    
    private void preProcessBST(TreeNode root){
        if(root == null){
            return;
        }
        //inorder traversal and populate valueArray
        preProcessBST(root.left);
        valueArray.add(root.val);
        preProcessBST(root.right);
    }
    
    private void postProcessBST(TreeNode root, List<Integer> values){
        if(root == null){
            return;
        }
        //inorder traversal and populate greater array values
        postProcessBST(root.left, values);
        root.val = values.get(index++);
        postProcessBST(root.right, values);
    }
}

```
