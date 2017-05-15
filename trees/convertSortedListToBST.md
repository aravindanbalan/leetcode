Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

```java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
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
    public TreeNode sortedListToBST(ListNode head) {
        if(head == null) return null;
        return sortedListToBSTUtil(head, null);
    }
    
    private TreeNode sortedListToBSTUtil(ListNode head, ListNode tail){
        if(head == tail) return null;
        ListNode slow = head;
        ListNode fast = head;
        
        while(fast!=tail && fast.next!=tail){
            fast = fast.next.next;
            slow = slow.next;
        }
        
        //now slow is in mid
        TreeNode root = new TreeNode(slow.val);
        root.left = sortedListToBSTUtil(head, slow);
        root.right = sortedListToBSTUtil(slow.next, tail);
        
        return root;
    }
}
```
