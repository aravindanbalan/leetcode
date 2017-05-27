Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

Note:
All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
For example, given candidate set [10, 1, 2, 7, 6, 1, 5] and target 8, 
A solution set is: 
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]

```java
public class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        
        List<List<Integer>> result = new ArrayList<>();
         Arrays.sort(candidates);
        int N = candidates.length;
        helper(candidates, new ArrayList<Integer>(), N, target, result, 0);
        
        return result;
    }
    
    private void helper(int[] candidates, List<Integer> tempList, int N, int newTarget, List<List<Integer>> result, int start){
        if(newTarget<0){
            return;
        }
        if(newTarget == 0){
            List<Integer> list = new ArrayList<>(tempList);
            result.add(list);
        }
        
        for(int i =start;i<N;i++){
            if(i > start && candidates[i] == candidates[i-1]) continue; //avoid duplicates
            int num = candidates[i];
                tempList.add(num);
                helper(candidates, tempList, N, newTarget - num, result, i+1);
                tempList.remove(tempList.size()-1);
        }
    }
}
```
