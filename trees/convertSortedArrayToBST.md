Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

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
    public TreeNode sortedArrayToBST(int[] nums) {
        if(nums.length == 0) return null;
        if(nums.length == 1) return new TreeNode(nums[0]);
        
        return sortArrayToBSTUtil(nums, 0, nums.length-1);
    }
    
    private TreeNode sortArrayToBSTUtil(int[] nums, int left, int right){
        if(left > right) return null;
        
        if(left == right){
            return new TreeNode(nums[left]);
        }
        
        int mid = left + (right-left)/2; //avoid integer overflow
        TreeNode root = new TreeNode(nums[mid]);
        
        root.left = sortArrayToBSTUtil(nums, left, mid-1);
        root.right = sortArrayToBSTUtil(nums, mid+1, right);
        
        return root;
        
    }
}
```

