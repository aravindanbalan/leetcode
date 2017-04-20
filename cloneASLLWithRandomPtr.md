```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if(head == null){
            return head; // empty list
        }
        
        RandomListNode iter = head;
        
        //duplicate nodes
        while(iter!=null){
            RandomListNode newNode = new RandomListNode(iter.label);
            RandomListNode nextNode = iter.next;
            newNode.next = nextNode;
            iter.next = newNode;
            iter = nextNode;
        }
        
        //clone pointers
        iter = head;
         while(iter!=null){
            if(iter.random!=null){
                iter.next.random = iter.random.next;
            }
             iter = iter.next.next;
        }
        
        iter = head;
        RandomListNode dummy = new RandomListNode(-1);
        RandomListNode copy, next, copyIterator = dummy;
        
        //restore original list and return cloned list
        while(iter!=null){
            next = iter.next.next;
            copy = iter.next;
            copyIterator.next = copy;
            copyIterator = copy;
            
            iter.next = next;
            iter = next;
        }
        
        return dummy.next;
    }
}
```
