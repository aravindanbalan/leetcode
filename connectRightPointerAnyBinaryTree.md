```
Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

Note:

You may only use constant extra space.
For example,
Given the following binary tree,
         1
       /  \
      2    3
     / \    \
    4   5    7
After calling your function, the tree should look like:
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL
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
     
        TreeLinkNode head = null;
        TreeLinkNode prev = null;
        TreeLinkNode curr = root;
        
        //level order traversal iterative
        while(curr!=null){
            while(curr!=null){
                if(curr.left!=null){
                    if(prev!=null){
                        prev.next = curr.left;
                    } else{
                        //first node encountered in this level
                        head = curr.left;
                    }
                    
                    //update previously encountered node in that level
                    prev = curr.left;
                }
                
                if(curr.right!=null){
                    if(prev!=null){
                        prev.next = curr.right;
                    }else{
                        //this is the first node in this level
                        head = curr.right;
                    }
                    //update previously encountered node in that level
                    prev = curr.right;
                }
                
                curr = curr.next; //move to next node in that level
            }
            
            //move to next level and reset values and start from scratch
            curr = head;
            head = null; 
            prev = null;
        }
    }
}
```
