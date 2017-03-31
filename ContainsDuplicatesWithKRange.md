Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.

```java
public class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        int n = nums.length;
        if(k ==0 || n==0||n==1) return false;  //k==0 as we need distinct indices
        
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        map.put(nums[0], 0);
        
        for(int i=1;i< n;i++){
            if(map.containsKey(nums[i])){
                int j = map.get(nums[i]);
                if(Math.abs(i-j) <=k){
                    return true;
                }else{
                    map.put(nums[i], i); //update latest occurence of nums[i]  , this is for test [1,0,1,1] & k = 1
                }
            } else{
                map.put(nums[i], i);
            }
        }
        return false;
    }
}

```
