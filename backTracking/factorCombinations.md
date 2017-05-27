```
Numbers can be regarded as product of its factors. For example,

8 = 2 x 2 x 2;
  = 2 x 4.
Write a function that takes an integer n and return all possible combinations of its factors.

Note: 
You may assume that n is always positive.
Factors should be greater than 1 and less than n.
Examples: 
input: 1
output: 
[]
input: 37
output: 
[]
input: 12
output:
[
  [2, 6],
  [2, 2, 3],
  [3, 4]
]
input: 32
output:
[
  [2, 16],
  [2, 2, 8],
  [2, 2, 2, 4],
  [2, 2, 2, 2, 2],
  [2, 4, 4],
  [4, 8]
]
```

```java
public class Solution {
    public List<List<Integer>> getFactors(int n) {
        if(n <=3) return new ArrayList<>(); 
        
        List<List<Integer>> result = new ArrayList<>();
        
        factorsUtil(n, new ArrayList<>(), result, 2);
        return result;
    }
    
    private void factorsUtil(int n, List<Integer> tempList, List<List<Integer>> result, int start){
        if(n <=0) return;
        
        if (n == 1) {
            if (tempList.size() > 1) {
                result.add(new ArrayList<Integer>(tempList));
            }
            return;
        }
        
        for(int i = start ; i<= n ;i++){
            if(n % i == 0){
                tempList.add(i);
                factorsUtil(n/i, tempList, result, i);
                tempList.remove(tempList.size() -1);
            }
        }
    }
}
```
