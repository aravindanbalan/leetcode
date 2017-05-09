
```
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

The update(i, val) function modifies nums by updating the element at index i to val.
Example:
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```

```java
public class NumArray {
    
    class SegmentTreeNode{
        int start, end;
        int sum;
        SegmentTreeNode left, right;
        
        public SegmentTreeNode(int start, int end){
            this.start = start;
            this.end = end;
            this.sum = 0;
            this.left = null; this.right = null;
        }
    }
    
    private SegmentTreeNode root = null;

    public NumArray(int[] nums) {
        root = buildSegmentTree(nums, 0, nums.length-1);
    }
    
    public void update(int i, int val) {
        update(root, i, val);
    }
    
    public int sumRange(int i, int j) {
        return sumRange(root, i, j);
    }
    
    private SegmentTreeNode buildSegmentTree(int[] nums, int start, int end){
        if(start > end){
            return null;
        }else{
            SegmentTreeNode root = new SegmentTreeNode(start, end);
            if(start == end){ //leaf node
                root.sum = nums[start];
            }else{
                int mid = (start + end)/2;
                root.left = buildSegmentTree(nums, start, mid);
                root.right = buildSegmentTree(nums, mid+1, end);
                root.sum = root.left.sum + root.right.sum;
            }
            
            return root;
        }
    }
    
    private void update(SegmentTreeNode root, int pos , int val){
        if(root.start == root.end){ //leaf node
            root.sum = val; //update val
        }else{
            int mid = (root.start + root.end)/2;
            if(pos <=mid){
                update(root.left, pos, val);
            }else{
                update(root.right, pos, val);
            }
            
            //update sum on the way up in case of changes
            root.sum = root.left.sum + root.right.sum;
        }
    }
    
    private int sumRange(SegmentTreeNode root, int start, int end){
        if(root.start == start && root.end == end){ //exact interval query (exact overlap)
            return root.sum;
        }else{
            int mid = (root.start + root.end)/2;
            if(end <= mid){ //if query is for the left
                return sumRange(root.left, start, end); //left tree
            }else if(start >=mid+1){ //query is on the right
                return sumRange(root.right, start, end);
            }else{
                //then we need sum of both trees
                return sumRange(root.left, start, mid) + sumRange(root.right, mid+1, end);
            }
        }
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(i,val);
 * int param_2 = obj.sumRange(i,j);
 */
```
