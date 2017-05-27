The gray code is a binary numeral system where two successive values differ in only one bit.

Given a non-negative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.

For example, given n = 2, return [0,1,3,2]. Its gray code sequence is:

00 - 0
01 - 1
11 - 3
10 - 2

```java
public class Solution {
    public List<Integer> grayCode(int n) {
        List<Integer> result = new ArrayList<Integer>();
        
        //gray code is one where consecutive numbers differ by a hamming distance of 1
        // Idea is : for any N we have 2N combinations with hamming distance 1
        // And to generate the next number we do i xor i/2 to get a number differing by 1 bit
        
        //so for each index of i we do i ^ (i>>1)
        
        for(int i = 0; i< (1<<n); i++){
            result.add(i ^ (i>>1));
        }
        
        return result;
    }
}
```
