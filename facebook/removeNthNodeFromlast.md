```
Given a linked list, remove the nth node from the end of list and return its head.

For example,

   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
```

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        //nothing to remove
        if(head == null) return head;
        //one node and it shud be removed
        if(head.next == null && n==1) return null;
        
        //nothing to be removed
        if(n == 0) return head;
          
        ListNode start = new ListNode(0);
        ListNode slow = start, fast = start;
        slow.next = head; //since all objects are refernce variables and its copied by value, so both fast.next and start.next will also be head
        
        //Move fast in front so that the gap between slow and fast becomes n
        for(int i=1; i<=n+1; i++)   {
            fast = fast.next;
        }
        //Move fast to the end, maintaining the gap
        while(fast != null) {
            slow = slow.next;
            fast = fast.next;
        }
        //Skip the desired Nth node
        slow.next = slow.next.next;
        return start.next;
    }
}
```
