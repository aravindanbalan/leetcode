Remove all elements from a linked list of integers that have value val.

Example
Given: 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, val = 6
Return: 1 --> 2 --> 3 --> 4 --> 5

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
    public ListNode removeElements(ListNode head, int val) {
        if(head == null){
            return head;
        }
        
        if(head.val == val && head.next == null){
            // single node deletion
            return null;
        }
        
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode tmp = dummy;
        
        while(tmp!=null){
            if(tmp.next!=null && tmp.next.val == val){
                tmp.next = tmp.next.next;
            }else{
                tmp = tmp.next; //advance the ptr
            }
        }
        return dummy.next;
    }
}
```
