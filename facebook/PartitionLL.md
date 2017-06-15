```
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given 1->4->3->2->5->2 and x = 3,
return 1->2->2->4->3->5.
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
    public ListNode partition(ListNode head, int x) {
        if(head == null) return null;
        if(head.next == null) return head;
        
        //kinda split and merge two lists
        
        ListNode dummy1 = new ListNode(-1);
        ListNode dummy2 = new ListNode(-1);
        ListNode curr1 = dummy1, curr2 = dummy2;
        
        while(head!=null){
            if(head.val < x){
                //add to list 1
                curr1.next = head;
                curr1 = curr1.next;
            }else{
                curr2.next = head;
                curr2 = curr2.next;
            }
            head = head.next;
        }
        
        curr2.next = null;
        curr1.next = dummy2.next;
        return dummy1.next;
        
    }
}
```
