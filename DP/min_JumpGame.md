```
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

For example:
Given array A = [2,3,1,1,4]

The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)
```
```java
public class Solution {
    public int jump(int[] nums) {
        if(nums.length <= 1) return 0;
        
        
        //Dynamic programming - O(n^2) time and O(n) space
        int[] jumps = new int[nums.length];
        jumps[0] = 0;
        
        for(int i = 1; i< nums.length ; i++){
            jumps[i] = Integer.MAX_VALUE;
        }
        
        //from index 1 to end
        for(int i = 1; i< nums.length ; i++){
            for(int j = 0; j< i; j++){
                //check if i can be reached from each of the indices before i
                if(j + nums[j] >= i){ //then can be reached
                    if(jumps[i] > jumps[j]+1){  //minimize
                        jumps[i] = jumps[j] + 1; 
                    }
                }
            }
        }
        
        return jumps[nums.length-1];
        
        
        //O(n) solution
        
        //Imagine this as building floor and at each floor we get a ladder of length i + nums[i].
        //we need to climb one ladder and then get a bigger ladder on the way.
        //once we reach the current ladder to the top we jump onto the next bigger ladder we picked
        
        int ladder = nums[0]; //ladder size
        int steps = nums[0]; //number of steps in that ladder
        int climb = 1;
        
        //for each floor
        for(int i = 1; i< nums.length ; i++){
            if(i == nums.length - 1){ //we reached last floor
                return climb;
            }
            
            //check ladder size at current level, if bigger pick up that ladder
            if(ladder < i + nums[i]) ladder = i + nums[i];
            
            steps--; //decrement number of steps climbed in old ladder
            
            if(steps == 0) { //once we climbed the older ladder completely, jump onto the bigger ladder picked up
                climb++;
                steps = ladder - i; //now number of steps remaining in the bigger ladder will be ladder length - the floor number we are in
            }
        }
        
        return climb;
    }
}
```
