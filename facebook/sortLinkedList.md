Sort a linked list in O(n log n) time using constant space complexity.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode sortList(ListNode head) {
        if(head == null || head.next == null) return head;
        
        ListNode prev = null;
        ListNode slow = head;
        ListNode fast = head;
        
        while(fast!=null && fast.next!=null){
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        
        //1. seperate into two lists
        prev.next = null;
        
        //now head and slow are two lists
        
        //2. Now recurse
        
        ListNode l1 = sortList(head);
        ListNode l2 = sortList(slow);
        
        //3. merge
        return merge(l1, l2);
    }
    
    private ListNode merge(ListNode l1, ListNode l2){
        ListNode dummy = new ListNode(-1);
        ListNode iter = dummy;
        
        while(l1!= null && l2!=null){
            if(l1.val < l2.val){
                iter.next = l1;
                l1 = l1.next;
            }else{
                iter.next = l2;
                l2 = l2.next;
            }
            
            iter = iter.next;
        }
        
        if(l1!=null) iter.next = l1;
        else if(l2!=null) iter.next = l2;
        
        return dummy.next;
    }
}
```
