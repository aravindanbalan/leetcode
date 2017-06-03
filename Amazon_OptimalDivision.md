```
Given a list of positive integers, the adjacent integers will perform the float division. For example, [2,3,4] -> 2 / 3 / 4.

However, you can add any number of parenthesis at any position to change the priority of operations. You should find out how to add parenthesis to get the maximum result, and return the corresponding expression in string format. Your expression should NOT contain redundant parenthesis.

Example:
Input: [1000,100,10,2]
Output: "1000/(100/10/2)"
Explanation:
1000/(100/10/2) = 1000/((100/10)/2) = 200
However, the bold parenthesis in "1000/((100/10)/2)" are redundant, 
since they don't influence the operation priority. So you should return "1000/(100/10/2)". 

Other cases:
1000/(100/10)/2 = 50
1000/(100/(10/2)) = 50
1000/100/10/2 = 0.5
1000/100/(10/2) = 2
```

```java
public class Solution {
    public String optimalDivision(int[] nums) {
        //always a/b/c/d  is equal to (a*c*d...) /b
        
        //1000/(100/10/2) = 1000/((100/10)/2) = 200
        //which can be writtern as (2*10*1000)/100 = 200
        
        if(nums.length == 0) throw new ArrayIndexOutOfBoundsException();
        
        StringBuilder sb = new StringBuilder();
        
        sb.append(Integer.toString(nums[0]));
        
        if(nums.length == 1) return sb.toString();
        if(nums.length == 2) return sb.append('/').append(Integer.toString(nums[1])).toString();
        
        sb.append("/(").append(Integer.toString(nums[1]));
        
        for(int i = 2; i< nums.length ; i++){
            sb.append('/').append(Integer.toString(nums[i]));
        }
        
        sb.append(')');
        
        return sb.toString();
    }
}
```
