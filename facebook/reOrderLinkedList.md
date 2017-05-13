```
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You must do this in-place without altering the nodes' values.

For example,
Given {1,2,3,4}, reorder it to {1,4,2,3}.
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
    public void reorderList(ListNode head) {
        if(head == null) return;
        if(head.next == null) return;
        
        ListNode slow = head, fast = head;
        
        //1. find the middle element 
        while(fast.next!=null && fast.next.next!=null){
            slow = slow.next;
            fast = fast.next.next;
        }
        
        //middle element will be slow now
        ListNode middle = slow;
        //2. reverse second half of the list  
        ListNode second = reverse(slow.next);
      
        //3. reset slow to head and fast to reverse list. Now merge both
        slow = head;
        fast = second;
        
        //for list 1->2->4->3, middle = 2, slow = 1, fast = 4
        while(slow!=middle){
            middle.next = fast.next; //2->3
            fast.next = slow.next; //4->2
            slow.next = fast; //1->4
            slow = fast.next; // 2
            fast = middle.next; //3
        }
    }
    
    private ListNode reverse(ListNode head){
        ListNode pre = null;
        while(head!=null){
            ListNode next = head.next;
            head.next = pre;
            pre = head;
            head = next;
        }
        return pre;
    }
}
```
