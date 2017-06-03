Given the root of a tree, you are asked to find the most frequent subtree sum. The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself). So what is the most frequent subtree sum value? If there is a tie, return all the values with the highest frequency in any order.

Examples 1
Input:

  5
 /  \
2   -3
return [2, -3, 4], since all the values happen only once, return all of them in any order.
Examples 2
Input:

  5
 /  \
2   -5
return [2], since 2 happens twice, however -5 only occur once.

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
    int maxCount;
    
    public int[] findFrequentTreeSum(TreeNode root) {
        if(root == null) return new int[]{};
        map = new HashMap<Integer, Integer>();

        findFrequentTreeSumUtil(root);
        
        List<Integer> temp = new ArrayList<>();
        
        for(Integer sum : map.keySet()){
            if(map.get(sum) == maxCount){
                temp.add(sum);
            }
        }
        
        int[] result = new int[temp.size()];
        int index = 0;
        for(int num : temp){
            result[index++] = num;
        }
        
        return result;
    }
    
    //Post order traversal calculating sum
    private int findFrequentTreeSumUtil(TreeNode root){
        if(root == null) return 0;
        
        int leftSum = findFrequentTreeSumUtil(root.left);
        int rightSum = findFrequentTreeSumUtil(root.right);
        
        int sum = leftSum + rightSum + root.val;
        int count = 1;
        
        if(map.containsKey(sum)){
            count = map.get(sum) +1;
        }
        
        map.put(sum, count);
        maxCount = Math.max(maxCount, count);
        
        return sum;
    }
}
```
