Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

Note: Do not modify the linked list.

Follow up:
Can you solve it without using extra space?

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if(head == null || head.next == null){
            return null;
        }
        
        ListNode slow = head;
        ListNode fast = head;
        boolean isCycle = false;
        
        while(slow.next!=null && fast.next!=null && fast.next.next!=null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow == fast){
                isCycle = true;
                break;
            }
        }
        
        if(!isCycle) return null;
        
        //reset one of the ptr to head of list and increment both by one step at a time to find the start of the cycle.
        slow = head;
        while(slow != fast){
            slow = slow.next;
            fast = fast.next;
        }
        
        return slow;
    }
}
```
