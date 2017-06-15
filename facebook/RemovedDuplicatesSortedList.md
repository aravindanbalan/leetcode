```
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,
Given 1->2->3->3->4->4->5, return 1->2->5.
Given 1->1->1->2->3, return 2->3.
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
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null) return head; //0 or 1 nodes
        
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        
        ListNode pre = dummy; //points to dummy node
        ListNode curr = head; // points to first node
        
        while(curr!=null){
            //move curr till next val is not duplicate, that is last node of repeating elements
            while(curr.next!=null && curr.val == curr.next.val)
                curr = curr.next;
                
            //no duplicates like -1->1->2
            if(pre.next == curr){
                pre = pre.next; //now points to 1
            }else{
                //-1->1->1->2, pre = -1, curr = last 1 
                pre.next= curr.next; //-1->2 skip everything
            }
            
            curr = curr.next;
        }
        
        return dummy.next;
    }
}
```
