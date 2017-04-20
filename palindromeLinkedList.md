
Given a singly linked list, determine if it is a palindrome.

Follow up:
Could you do it in O(n) time and O(1) space?

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
    public boolean isPalindrome(ListNode head) {
        if(head == null){
            return true;
        }
        
        if(head.next==null){
            return true;
        }
        
        ListNode fast = head;
        ListNode slow= head;
        
        while(fast!=null && fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
        }
        
        if(fast!=null) {
            //odd number of nodes
            slow = slow.next; //now slow refers to the mid point of the list
        }
        
        slow = reverse(slow);
        fast = head;
        
        while(slow!=null){
            if(fast.val != slow.val){
                return false;
            }
            
            fast = fast.next;
            slow = slow.next;
        }
        
        return true;
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
