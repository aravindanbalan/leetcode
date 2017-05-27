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
         //to eliminate duplicates, we first sort and then check inside the loop
         //if(i > start && candidates[i] == candidates[i-1]) continue; //avoid duplicates

        int N = candidates.length;
        helper2(candidates, new ArrayList<Integer>(), N, target, result, 0);
        
        return result;
    }
    
    private void helper(int[] candidates, List<Integer> tempList, int N, int newTarget, List<List<Integer>> result, int start){
        if(newTarget<0){
            return;
        }
        if(newTarget == 0){
            List<Integer> list = new ArrayList<>(tempList);
            result.add(list);
            return;
        }
        
        for(int i =start;i<N;i++){
            if(i > start && candidates[i] == candidates[i-1]) continue; //avoid duplicates
            int num = candidates[i];
                tempList.add(num);
                helper(candidates, tempList, N, newTarget - num, result, i+1);
                tempList.remove(tempList.size()-1);
        }
    }
    
    //More pruning by returning a flag
    //For example: the list is [1, 1, 2, 5, 6, 7, 10], target is 8 and the current list is [1, 1, 2]. Now we are at 5, and we know that [1, 1, 2, 5] will be greater than 8. The next to check is [1, 1, 2, 6]. However, we should already know that [1, 1, 2, 6] cannot work since [1, 1, 2, 5] already has a sum larger than 8. There is no need to check for [1, 1, 2, 6] or [1, 1, 2, 7] and so no.

    //Thus, when we find a match or the current sum is already larger than the target, we should not continue with the current list.
    private boolean helper2(int[] candidates, List<Integer> tempList, int N, int newTarget, List<List<Integer>> result, int start){
        if(newTarget<0){
            return true;
        }
        if(newTarget == 0){
            List<Integer> list = new ArrayList<>(tempList);
            result.add(list);
            return true;
        }
        
        for(int i =start;i<N;i++){
            if(i > start && candidates[i] == candidates[i-1]) continue; //avoid duplicates
            int num = candidates[i];
                tempList.add(num);
                boolean prune = helper2(candidates, tempList, N, newTarget - num, result, i+1);
                tempList.remove(tempList.size()-1);
                if(prune){
                    break;
                }
        }
        return false;
    }
}
```
