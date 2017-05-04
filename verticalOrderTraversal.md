```java
//Using DFS and Horizontal distance based map

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
    public List<List<Integer>> verticalOrder(TreeNode root) {
        
        //since problem
        Map<Integer, List<Integer>> map = new TreeMap<Integer, List<Integer>>();
        List<List<Integer>> result = new ArrayList<>();
        if(root == null) return result;
        
        verticalOrderUtil(root, 0, map);
        for(Map.Entry<Integer, List<Integer>> entry : map.entrySet()){
            result.add(new ArrayList<>(entry.getValue()));
        }
        return result;
    }
    
    private void verticalOrderUtil(TreeNode root, int hd, Map<Integer, List<Integer>> map){
        
        if(root == null) return;
        
        if(!map.containsKey(hd)){
            map.put(hd, new ArrayList<Integer>());
        }
        
        map.get(hd).add(root.val);
        //horizontal distance based map storage
        verticalOrderUtil(root.left, hd-1, map);
        verticalOrderUtil(root.right, hd+1, map);
    }
}
```
