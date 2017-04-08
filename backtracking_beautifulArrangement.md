Suppose you have N integers from 1 to N. We define a beautiful arrangement as an array that is constructed by these N numbers successfully if one of the following is true for the ith position (1 ≤ i ≤ N) in this array:

The number at the ith position is divisible by i.
i is divisible by the number at the ith position.
Now given N, how many beautiful arrangements can you construct?


```java
public class Solution {
    int count = 0;
    public int countArrangement(int N) {
        //if a method signature is like this for back tracking, then use a helper function to accept more input parameters
        //often you might require an array[] to store the recursive states for the next call
        
        if(N ==0) return 0;
        
        helper(1, N, new boolean[N+1]);
        return count;
    }
    
    private void helper(int pos, int N , boolean[] used){
        if(pos > N){
            count++; //we have reached our end goal so increment the count
            return;
        }
        
        for(int i = 1;i<=N;i++){
            if(used[i]==false && (i%pos == 0 || pos%i == 0)){
                used[i] = true;
                helper(pos+1, N, used);
                used[i] = false;
            }
        }
    }
}

```
