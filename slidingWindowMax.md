```java
Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

For example,
Given nums = [1,3,-1,-3,5,3,6,7], and k = 3.

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
Therefore, return the max sliding window as [3,3,5,5,6,7].
```

```java
public class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        
        //Working solution with heap
        if(nums.length == 0)
            return new int[]{};
            
        PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(k, new Comparator<Integer>(){
            @Override
            public int compare(Integer a, Integer b){
                return -1 * a.compareTo(b);
            }
        });
        
        int n= nums.length;
        int[] max = new int[n-k+1];
        Arrays.fill(max, Integer.MIN_VALUE);
        
        for(int i =0;i< k; i++){
            maxHeap.add(nums[i]);
            
            if(max[0] < nums[i]){
                max[0] = nums[i];
            }
        }
        
        int i = 1;
        while(i < n-k+1){
            maxHeap.remove(nums[i-1]); //sliding window so previous element goes off from heap
            maxHeap.add(nums[i+k-1]); //add new element
            max[i] = maxHeap.peek();
            i++;
        }
        
        return max;

    }
}
```
