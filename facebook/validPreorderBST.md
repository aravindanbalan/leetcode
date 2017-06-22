```java
public class Solution {
    public boolean verifyPreorder(int[] preorder) {
        if(preorder.length <=1) return true; //zero nodes or single nodes
        
        Stack<Integer> stack = new Stack<Integer>();
        int low = Integer.MIN_VALUE;
        
        //for [5,3,2,4,7,6]  - valid BST
        //for [5,3,2,4,1,6] - invalid BST
        for(int num : preorder){
            if(num < low) return false;
            
            while(!stack.isEmpty() && num > stack.peek())
                low = stack.pop(); //after 4 , low will be 3
            
            stack.push(num);
        }
        
        return true;
    }
}
```
