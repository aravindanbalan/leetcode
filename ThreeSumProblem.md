Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? 
Find all unique triplets in the array which gives the sum of zero.

```java
public class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        if(nums == null || nums.length < 3){
            return new ArrayList<>();
        }
        
        //important step is to sort the array, otherwise this algorithm wont work
        Arrays.sort(nums);  //O(nlogn)
        
        List<List<Integer>> result = new ArrayList<>();
        
        for(int i = 0;i < nums.length - 2; i++){  // O(n)
            
            if(i == 0 || nums[i] > nums[i-1]){
                int begin = i+1;
                int end = nums.length-1;
                
                while(begin < end){   //O(n)
                    int sum = nums[i] + nums[begin] + nums[end];
                    
                    if(sum == 0){
                        List<Integer> list = new ArrayList<Integer>();
                        list.add(nums[i]); list.add(nums[begin]); list.add(nums[end]);
                        result.add(list);
                        begin++;
                        end--;
                        
                        while(begin < end && nums[begin] == nums[begin-1]) begin++;
                        while(begin < end && nums[end] == nums[end+1]) end--;
                    }else if(sum < 0){
                        begin++;
                    }else{
                        end--;
                    }
                }
            }
        }
        
        return result;
    }
}

//Total complexity  : O(nlogn) + O(n^2) = O(n^2)
//Naive complexity : O(n^3)
```
