 ```
 The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Now your job is to find the total Hamming distance between all pairs of the given numbers.

Example:
Input: 4, 14, 2

Output: 6

Explanation: In binary representation, the 4 is 0100, 14 is 1110, and 2 is 0010 (just
showing the four bits relevant in this case). So the answer will be:
HammingDistance(4, 14) + HammingDistance(4, 2) + HammingDistance(14, 2) = 2 + 2 + 2 = 6.
 ```
 
 ```java
 public class Solution {
    public int totalHammingDistance(int[] nums) {
        // if(nums.length < 2) return 0;
        
        // int xor = nums[0];
        // for(int i = 1; i< nums.length; i++){
        //     xor ^= nums[i];
        // }
        
        // int sum = 0;
        // for(int i = 0;i< nums.length; i++){
        //     int tempXor = xor ^ nums[i];
        //     sum += Integer.bitCount(tempXor);
        // }
        
        // return sum;
        
        //The above will take a lot of time to calculate
        
        //If you take each position and say k numbers in nums has a set bit 1 and other n-k has 0, then it contributes k * (n-k) to the result count since we take pairs
        
        int total = 0;
         //for each position in a 32 bit integer
        for(int i = 0; i< 32; i++){
            int bitCount = 0;
            for(int num : nums)
                bitCount += (num >> i) & 1; //check for set bit at ith position
                
            total += bitCount * (nums.length - bitCount);
        }
        
        return total;
    }
}
 ```
