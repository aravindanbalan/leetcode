You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if(l1 == null) return l2;
        if(l2 == null) return l1;
        
        int carry = 0;
        ListNode dummy = new ListNode(-1);
        ListNode iter = dummy;
        
        while(l1!=null && l2!=null){
            int sum = l1.val + l2.val + carry;
            if(sum < 10){
                iter.next = new ListNode(sum);
                carry =0;
            }else{
                iter.next = new ListNode(sum%10);
                carry = 1;
            }
            l1 = l1.next; l2 = l2.next; iter = iter.next;
        }
        
        if(l1 == null && l2 == null){
            if(carry == 1){
                iter.next = new ListNode(carry);
            }
            return dummy.next;
        }
        
        ListNode rem = (l1 == null)?l2 : l1;
        
        while(rem!=null){
            int sum = rem.val + carry;
            if(sum < 10){
                iter.next = new ListNode(sum);
                carry  = 0;
            }else{
                iter.next = new ListNode(sum%10);
                carry = 1;
            }
            iter = iter.next;
            rem = rem.next;
        }
        
       if(carry == 1){
            iter.next = new ListNode(carry);
        }
        
        return dummy.next;
    }
}
```
