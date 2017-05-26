Given a collection of distinct numbers, return all possible permutations.

For example,
[1,2,3] have the following permutations:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
Hide Company Tags

```java

public class Solution {
    public List<List<Integer>> permute(int[] nums) {
        if(nums.length == 0){
            return new ArrayList<>();
        }
        
        List<List<Integer>> result = new ArrayList<>();
        
        permuteUtil(nums, new ArrayList<Integer>(), result, new boolean[nums.length]);
        return result;
    }
    
    private void permuteUtil(int[] nums, List<Integer> tempList, List<List<Integer>> result, boolean[] used){
        if(tempList.size() == nums.length){
            //we have a result
            result.add(new ArrayList<>(tempList));
            return;
        }
        
        for(int i = 0; i < nums.length; i++){
            if(used[i]) continue;
            
            used[i] = true;
            tempList.add(nums[i]);
            permuteUtil(nums, tempList, result, used);
            tempList.remove(tempList.size() - 1);
            used[i] = false;
        }
    }
}
```
