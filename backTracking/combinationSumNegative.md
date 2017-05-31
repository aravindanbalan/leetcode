```java
/* Find all subsets of size k in an array that sum up to target 
the array may contains negative number */ 
class Solution { 

public List<List<Integer>> combinationSum(int[] nums, int target, int k) { 

}
}

https://www.careercup.com/question?id=5733553401757696

```java
import java.util.ArrayList;
import java.util.List;

/**
 * Created by arbalan on 5/30/17.
 */
public class CombinationSumFB {

    public static List<List<Integer>> combinationSum(int[] nums, int target, int k){
        if(nums.length == 0 || k ==0)
                return new ArrayList<List<Integer>>();

        List<List<Integer>> result = new ArrayList<List<Integer>>();
        combinationSumUtil(nums, k, 0, target, new ArrayList<Integer>(), result);

        return result;
    }

    public static void combinationSumUtil(int[] nums, int k, int start, int target, List<Integer> tempList, List<List<Integer>> result) {

        if(k < 0) return;
        if(k == 0 && target == 0){
            result.add(new ArrayList<Integer>(tempList));
            return;
        }

        for(int i = start; i< nums.length; i++){
            tempList.add(nums[i]);
            combinationSumUtil(nums, k - 1, i + 1, target - nums[i], tempList, result);
            tempList.remove(tempList.size()-1);
        }
    }

    public static void main(String args[]){
       int[] nums = {-1,2,-2,3,4,1};
        List<List<Integer>> result = combinationSum(nums, 3, 2);

        System.out.print(result.toString());
    }
}

```

```
