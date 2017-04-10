```
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:
Given the below binary tree and sum = 22,
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
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
    List<List<Integer>> result;
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        
        if(root == null) return new ArrayList<>();
        result = new ArrayList<>();
        pathSumUtil(root, result, new ArrayList<Integer>(), sum);
        return result;
    }
    
    private void pathSumUtil(TreeNode root, List<List<Integer>> result, List<Integer> tempList, int sum){
        if(root == null) return;
                
        tempList.add(root.val);

        if(root.val == sum && root.left == null && root.right == null){
            //leaf node and we have a result
            result.add(new LinkedList<>(tempList)); //Looks like we need to create a new list from existing list
            tempList.remove(tempList.size()-1);
            return;
        }    
         
        pathSumUtil(root.left, result, tempList, sum - root.val);
        pathSumUtil(root.right, result, tempList, sum - root.val);
        tempList.remove(tempList.size() - 1);
    }
}
```
