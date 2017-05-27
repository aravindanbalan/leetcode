Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:

[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]

```java
public class Solution {
    public List<List<Integer>> combine(int n, int k) {
        if(n==0 || k==0 || k > n) return new ArrayList<>();
        
        List<List<Integer>> result = new ArrayList<>();
        
        combineUtil(n, k, 1, new ArrayList<Integer>(), result);
        
        return result;
    }
    
    private void combineUtil(int n, int k, int start, List<Integer> tempList, List<List<Integer>> result){
        if(tempList.size() == k){
            result.add(new ArrayList<>(tempList));
            return;
        }
        
        for(int i = start ; i<=n ;i++){
            tempList.add(i);
            combineUtil(n, k, i+1, tempList, result);
            tempList.remove(tempList.size() -1);
        }
    }
}
```
