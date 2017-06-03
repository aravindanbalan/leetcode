Design a data structure that supports all following operations in average O(1) time.

insert(val): Inserts an item val to the set if not already present.
remove(val): Removes an item val from the set if present.
getRandom: Returns a random element from current set of elements. Each element must have the same probability of being returned.

```java
public class RandomizedSet {

   Random random;
   List<Integer> nums;
   Map<Integer, Integer> locs; //location map
   
    public RandomizedSet() {
        random = new Random();
        //We need an array list as get(index) is O(1) time
        nums = new ArrayList<Integer>();
        locs = new HashMap<Integer, Integer>();
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        boolean contains = locs.containsKey(val);
        if(contains) return false;
        
        locs.put(val, nums.size()); //initially 0, so loc points to 0
        nums.add(val); //now size is 1
        return true;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        boolean contains = locs.containsKey(val);
        if(!contains) return false;
        
        int loc = locs.get(val);
        if(loc < nums.size() -1){
            int lastVal = nums.get(nums.size() -1); //get last element
            nums.set(loc, lastVal); //move the last value in this loc and later delete the last one  - O(1)
            locs.put(lastVal, loc); //update the loc of last value
        }
       
        locs.remove(val); //O(1)
        nums.remove(nums.size() -1); //remove the last element - O(1)
        
        return true;
    }
    
    /** Get a random element from the set. */
    public int getRandom() {
        return nums.get(random.nextInt(nums.size()));
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```
