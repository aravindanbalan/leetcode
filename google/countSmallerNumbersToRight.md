```
You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

Example:

Given nums = [5, 2, 6, 1]

To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
Return the array [2, 1, 1, 0].
```


```java
public class Solution {
    public List<Integer> countSmaller(int[] nums) {
        //Naive solution is two for loops and find count of numbers greater than this number O(n^2)
        
        //BST solution : O(nlogn)
        int n = nums.length;
        if(n==0) return new ArrayList<Integer>();
        
        BstTreeNode root = new BstTreeNode(nums[n-1]);
        Integer[] count = new Integer[n];
        count[n-1] = 0;
        for(int i = n-2; i>=0; i--){
            count[i] = insert(root, nums[i]);
        }
        
        return Arrays.asList(count);
    }
    
    private int insert(BstTreeNode root, int val){
        if(val < root.val){
            //it should be inserted on the left sub tree
            root.leftNodeCount++;
            if(root.left !=null){
                return insert(root.left, val);
            }
            
            //else insert new node to the left
            root.left = new BstTreeNode(val);
            return 0; //return count as leftNodeCount as thats what is needed as result
        }else if(val > root.val){
            //should be inserted on the right node
            int smallerCount = root.leftNodeCount + root.dup; // duplicates count + left node count
            if(root.right !=null){
                return insert(root.right, val) + smallerCount;
            }
            
            //else insert the node on the right subtree
            root.right = new BstTreeNode(val);
            return smallerCount;
        }else{
            //duplicate as root
            root.dup++;
            return root.leftNodeCount;
        }
    }
    
    class BstTreeNode{
        int val;
        int leftNodeCount;  //count of all nodes lesser than this node
        int dup = 1;
        BstTreeNode left, right;
        public BstTreeNode(int val){
            this.val = val;
        }
    }
}

```
