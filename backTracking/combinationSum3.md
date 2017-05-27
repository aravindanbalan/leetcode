Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.


Example 1:

Input: k = 3, n = 7

Output:

[[1,2,4]]

Example 2:

Input: k = 3, n = 9

Output:

[[1,2,6], [1,3,5], [2,3,4]]

```java
public class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        
        if(k == 0 || n==0) return new ArrayList<>();
        
        boolean[] used = new boolean[10];
        List<List<Integer>> result = new ArrayList<>();
        
        //combination we shud always use start and in for loop i+1 so that its not chosen again.
        //To remove duplicates if given array, we sort and check i > start && combi[i] != combi[i-1]
        combinationSumUtil(k , n, 1, used, new ArrayList<Integer>(), result);
        return result;
    }
    
    private void combinationSumUtil(int k, int targetSum, int start, boolean[] used, List<Integer> tempList, List<List<Integer>> result){
        if(targetSum < 0 || k < 0) return;
        if(targetSum == 0 && k == 0){
            result.add(new ArrayList<>(tempList));
            return;
        }
        
        for(int i = start ; i<=9; i++){
            used[i] = true;
            tempList.add(i);
            combinationSumUtil(k-1, targetSum - i, i+1, used, tempList, result);
            tempList.remove(tempList.size() - 1);
            used[i] = false;
        }
    }
}
```
