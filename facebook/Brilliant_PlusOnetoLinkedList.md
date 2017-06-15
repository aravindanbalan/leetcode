```
Given a non-negative integer represented as non-empty a singly linked list of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

Example:
Input:
1->2->3

Output:
1->2->4
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
    public ListNode plusOne(ListNode head) {
        if(head == null) return null;
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode i = dummy;  //i represents the last whose val != 9
        ListNode j = dummy;
        
        while(j.next!=null){ //go till the last node
            j = j.next;
            if(j.val != 9) i = j;
        }
        
        //check last node val
        if(j.val != 9){
            j.val++;
        }else{
            i.val++; //if dummy was the only non 9 value incase of 999, then dummy will become 1 
            
            i = i.next;
            //set reset to zero eg: 999 + 1 = 1000
            while(i!= null){
                i.val = 0;
                i = i.next;
            }
        }
        
        //check if dummy is still zero
        if(dummy.val == 0) return dummy.next; //case 0->1->2->3 to 0->1->2->4
        
        return dummy;
    }
}
```
