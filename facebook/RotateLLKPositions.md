```
Given a list, rotate the list to the right by k places, where k is non-negative.

For example:
Given 1->2->3->4->5->NULL and k = 2,
return 4->5->1->2->3->NULL.
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
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null || k<=0) return head;
        if(head.next == null) return head;
        
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        
        ListNode slow = dummy, fast = dummy;
        
        int len = 0;
        while(fast.next!=null){
            fast = fast.next;
            len++;
        }
        
        //now i represents the length of the list
        
        //if list 1-2-3 and k = 5, then we need to rotate after 3-5%3 =1 which is len - (k % len)
        //here rotate after 1st node
        
        //> 0 as we need to move slow by just 1 time. next time loop should not execute
        for(int i = 0; i< len - (k % len); i++){
            slow = slow.next;
        }
        
        //rotate
        //now fast = 3 and slow = 1 and dummy = -1
        fast.next = dummy.next; //3->1
        dummy.next = slow.next; //-1->2
        slow.next = null;  //1->null
        
        return dummy.next;
    }
}
```
