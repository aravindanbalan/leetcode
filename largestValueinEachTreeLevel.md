```
You need to find the largest value in each row of a binary tree.

Example:
Input: 

          1
         / \
        3   2
       / \   \  
      5   3   9 

Output: [1, 3, 9]
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
    Map<Integer, Integer> map;
    public List<Integer> largestValues(TreeNode root) {
        if(root == null){
            return new ArrayList<Integer>();
        }
       
       List<Integer> result = new ArrayList<>();
       map = new HashMap<Integer, Integer>();
       largestValuesUtil(root, 0);
       
       for(Map.Entry valueEntry : map.entrySet()){
           result.add((int)valueEntry.getValue());
       }
       
       return result;
    }
    
    private void largestValuesUtil(TreeNode root, int depth){
        if(root == null){
            return;
        }
        
        if(map.containsKey(depth)){
            if(root.val > map.get(depth)){
                map.put(depth, root.val);
            }
        }else{
            map.put(depth, root.val);
        }
        
        largestValuesUtil(root.left, depth+1);
        largestValuesUtil(root.right, depth+1);
    }
}
```
