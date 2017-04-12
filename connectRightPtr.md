```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

Note:

You may only use constant extra space.
You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).
For example,
Given the following perfect binary tree,
         1
       /  \
      2    3
     / \  / \
    4  5  6  7
After calling your function, the tree should look like:
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL
```


```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        if(root == null)
            return;
            
        TreeLinkNode levelPtr = root;
        while(levelPtr!=null){
            TreeLinkNode curr = levelPtr;
            
            while(curr!=null){
                if(curr.left!=null)     //connect 2 and 3 case
                    curr.left.next = curr.right;
                    
                if(curr.right!=null && curr.next !=null)  //connect 5 and 6 when curr is at 2
                    curr.right.next = curr.next.left;
                    
                curr = curr.next;
            }
            
            //move to next level
            levelPtr = levelPtr.left;
        }
    }
}
```
