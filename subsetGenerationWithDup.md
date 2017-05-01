Given a set of distinct integers, nums, return all possible subsets.

For example,
If nums = [1,2,3], a solution is:

[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
Hide Company Tags

```java
public class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        subsetUtil(nums, 0, new ArrayList<Integer>(), result);
        return result;
    }
    
    public void subsetUtil(int[] nums, int start, List<Integer> tempResult, List<List<Integer>> result){
        result.add(new ArrayList<Integer>(tempResult));
        
        for(int i = start; i < nums.length; i++){
            tempResult.add(nums[i]);
            subsetUtil(nums, i+1, tempResult, result);
            tempResult.remove(tempResult.size()-1);
        }
    }
}
```
