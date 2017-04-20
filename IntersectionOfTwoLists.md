```
Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:

A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
begin to intersect at node c1.
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null){  //one of the list is empty, then there is no intersection
            return null; 
        }
        
        int len1 = 0;
        int len2 = 0;
        
        ListNode list1 = headA;
        ListNode list2 = headB;
        
        for(;list1!=null;len1++, list1 = list1.next);

        for(;list2!=null;len2++, list2 = list2.next);
        
        while (len1 > len2) {
            headA = headA.next;
            len1--;
        }
         
        while(len1 < len2){
            headB = headB.next;
            len2--;
        } 
         
        while(headA != headB){
            headA = headA.next;
            headB = headB.next;
        }
        
        return headA;
    }
}
```
