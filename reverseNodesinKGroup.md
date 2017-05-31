Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

You may not alter the values in the nodes, only nodes itself may be changed.

Only constant memory is allowed.

For example,
Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5


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
    public ListNode reverseKGroup(ListNode head, int k) {
        if(head == null || k <=1) return head; //no need to reverse at all
        
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        
        ListNode prev = dummy, tail = dummy;
        ListNode temp;
        int i;
        
        while(true){
            i = 0;
            while(i < k && tail!=null){
                tail = tail.next;
                i++;
            }
            
            //we have reached end of list, we dont have the next set of k nodes to reverse
            if(tail == null) break;
            
            //if list is -1->1->2->3->4->5
            //prev = -1; tail = 3
            head = prev.next; //head = 1
            
            while(prev.next != tail){
                temp = prev.next; //assign  temp = 1
                prev.next = temp.next; //delete         -1->2
                temp.next = tail.next;                 //1->4
                tail.next = temp; //insert after tail   3->1
            }
            
            // list becomes -1->3->2->1->4->5
            prev = head; // prev = 1 now head = 1 is at the end
            tail = head; //tail = 1
        }
        
        return dummy.next;
    }
}

```
