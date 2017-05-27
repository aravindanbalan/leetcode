Given a collection of integers that might contain duplicates, nums, return all possible subsets.

Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,2], a solution is:

[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]

```java
public class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
       if(nums.length == 0) return new ArrayList<>();
       
       List<List<Integer>> result = new ArrayList<>();
       Arrays.sort(nums);
       subsetUtil(nums, 0, new ArrayList<Integer>(), result);
       
       return result;
    }
    
    private void subsetUtil(int[] nums, int start, List<Integer> tempList, List<List<Integer>> result){
        result.add(new ArrayList<>(tempList));
        
        for(int i = start; i< nums.length; i++){
            if(i > start && nums[i] == nums[i-1]) continue; //avoid duplicates
            tempList.add(nums[i]);
            subsetUtil(nums, i+1, tempList, result);
            tempList.remove(tempList.size() -1);
        }
    }
}
```
