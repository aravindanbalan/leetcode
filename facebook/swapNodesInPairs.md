Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

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
    public ListNode swapPairs(ListNode head) {
        if(head == null){
            return head;
        }
        
        //one node, dont swap as their is no pair
        if(head.next == null)
            return head;
            
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        
        ListNode pre = dummy;
        ListNode first = dummy.next;
        ListNode second = first.next;
        
        while(first!=null && second!=null){
            ListNode next = second.next;
            first.next = next;
            second.next = first;
            pre.next = second;
            pre = first;
            first = next;
            
            //if first is null then break
            if(first == null) break;
            //else
            second = first.next;
        }
        
        return dummy.next;
    }
}
```
