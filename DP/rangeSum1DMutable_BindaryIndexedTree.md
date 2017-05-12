Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

The update(i, val) function modifies nums by updating the element at index i to val.
Example:
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8


```java

    /** Approach using Binary Indexed Tree
     **/

    int[] BIT;
    int[] nums;

    public NumArray(int[] nums) {
        this.nums = nums;
        createBIT(nums);
    }
    
    public void update(int i, int val) {
        int diff = val - nums[i];
		nums[i] = val;
		//update i+1 index inside BIT
        updateBIT(BIT, diff, i+1);
    }
    
    public int sumRange(int i, int j) {
        return getSum(BIT, j) - getSum(BIT, i-1);  // sum (0...j) - sum(0...i-1) = sum(i...j) 
    }
    
    private void createBIT(int[] nums){
        BIT = new int[nums.length+1]; //BIT has n+1 elements
        for(int i = 1; i<=nums.length;i++){
            updateBIT(BIT, nums[i-1], i);
        }
    }
    
    private void updateBIT(int[] BIT, int val, int index){
        while(index < BIT.length){
            BIT[index] += val;
            index = getNext(index);
        }
    }
    
    private int getSum(int[] BIT, int index){
        index = index +1; //BIT stores values only from 1 to n
        int sum = 0;
        while(index > 0){
            sum += BIT[index];
            index = getParent(index);
        }
        
        return sum;
    }
    
    
    //helper methods for parent and next index
    private int getParent(int index){
        return index - (index & -index); 
    }
    
    private int getNext(int index){
        return index + (index & -index);
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(i,val);
 * int param_2 = obj.sumRange(i,j);
 */
```
