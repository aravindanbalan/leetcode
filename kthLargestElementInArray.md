Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

For example,
Given [3,2,1,5,6,4] and k = 2, return 5.

Note: 
You may assume k is always valid, 1 ≤ k ≤ array's length.


```java

public class Solution {
    public int findKthLargest(int[] nums, int k) {
        
        if(nums.length == 0) {
            return -1;
        }
        
        PriorityQueue<Integer> pq = new PriorityQueue<Integer>();  //minHeap
        
        for(int num : nums){
            pq.offer(num);
            if(pq.size() > k){
                pq.poll(); //removed the minimum most element in the array
            }
        }
        
        return pq.peek();
    }
}
```
