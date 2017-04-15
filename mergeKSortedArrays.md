Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

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
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null) return null;
        int n = lists.length;
        
        if(n==0) return null;
        if(n==1) return lists[0];
        
        ListNode result= null;
        PriorityQueue<ListNode> minHeap = new PriorityQueue<ListNode>(n, new Comparator<ListNode>(){
            @Override
            public int compare(ListNode a, ListNode b){
                return ((Integer)a.val).compareTo((Integer)b.val); //min Heap
            }
        });
        
        for(ListNode head : lists){
            if(head!=null){
                minHeap.add(head);
            }
        }
        
        ListNode dummy = new ListNode(0);
        ListNode tail=dummy;
        
        while(!minHeap.isEmpty()){
           tail.next = minHeap.poll();
            tail= tail.next;
            
            if(tail.next!=null){
                minHeap.add(tail.next);
            }
        }
        
        return dummy.next;
    }
}

```
