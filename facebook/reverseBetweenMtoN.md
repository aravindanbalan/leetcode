Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.

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
    public ListNode reverseBetween(ListNode head, int m, int n) {
        
        if(head == null) return null;
        if(n-m == 0) return head;
        
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        
        //pre will point to previous node of m
        ListNode pre = dummy;
        
        for(int i = 0; i< m-1;i++){
            pre = pre.next;
        }
        
        ListNode start = pre.next; //next Node to pre
        ListNode then = start.next; //next node to start
        
        //basically rotating the list. Take then and put after pre and shift nodes
        for(int i = 0; i< n-m ;i++){
            start.next = then.next;
            then.next = pre.next;
            pre.next = then;
            then = start.next;
        }
        return dummy.next;
    }
}
```
