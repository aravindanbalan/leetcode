You are given two integer arrays nums1 and nums2 sorted in ascending order and an integer k.

Define a pair (u,v) which consists of one element from the first array and one element from the second array.

Find the k pairs (u1,v1),(u2,v2) ...(uk,vk) with the smallest sums.

```java
public class Solution {
    public List<int[]> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        
        if(nums1.length == 0 || nums2.length == 0 || k ==0) return new ArrayList<>();
        
        //Idea : we need sum of pairs to be minimum
        //We need a heap which can store sum in min order - accessing min - O(1)
        //we need to store the next pointer of next item
        //First store all combination of items from first array and beginning ele of second
        
        PriorityQueue<int[]> minHeap = new PriorityQueue<int[]>(nums1.length, new Comparator<int[]>(){
            @Override 
            public int compare(int[] a, int[] b){
                //smallest sum
                return (a[0] + a[1]) - (b[0] + b[1]);
            }
        });
        
        List<int[]> result = new ArrayList<int[]>();
        
        //Add only k elements or nums1.length elements which ever is lower 
        //time : O(k Logn)  - logn for add elements to minHeap
        for(int i = 0; i < nums1.length && i < k; i++){
            //we store first ele from nums1 , second ele to be first element from nums2 and then we store next index in second
            minHeap.add(new int[]{nums1[i], nums2[0], 1});
        }
        
        int i =0;
        while(i < k && !minHeap.isEmpty()){
            int[] nums = minHeap.poll();
            result.add(new int[]{nums[0], nums[1]});
            
            if(nums[2] < nums2.length){
                minHeap.offer(new int[]{nums[0], nums2[nums[2]], nums[2]+1});
            }
            i++;
        }
        
        return result;
    }
}
```
