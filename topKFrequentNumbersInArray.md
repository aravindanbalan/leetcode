Given a non-empty array of integers, return the k most frequent elements.

For example,
Given [1,1,1,2,2,3] and k = 2, return [1,2].

Note: 
You may assume k is always valid, 1 ≤ k ≤ number of unique elements.  This gives us a hint that, its ```Range sorting ``` and it should be 
```Bucket sort``` or ```counting sort```.
Your algorithm's time complexity must be better than O(n log n), where n is the array's size 

```Bucket sort``` or ```counting sort``` complexity is O(n+k) where k is the number of buckets.

```java

public class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        List<Integer>[] buckets = new List[nums.length + 1]; //create nums.length buckets
        Map<Integer, Integer> frequencyMap = new HashMap<Integer, Integer>();
        
        for(int i =0;i<nums.length;i++){
            if(frequencyMap.containsKey(nums[i])){
                frequencyMap.put(nums[i] , frequencyMap.get(nums[i]) + 1);
            }else{
                frequencyMap.put(nums[i], 0);
            }
        }
        
        for(int key : frequencyMap.keySet()){
            int frequency = frequencyMap.get(key);
            if(buckets[frequency] == null){
                buckets[frequency] = new ArrayList<Integer>();
            }
            
            buckets[frequency].add(key);
        }
        
        List<Integer> res = new ArrayList<>();
        for(int pos = buckets.length - 1 ; pos >= 0 && res.size() < k ; pos--){
            if(buckets[pos]!=null){
                res.addAll(buckets[pos]);
            }
        }
        
        return res;
    }
}
```
