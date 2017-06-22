```
One way to serialize a binary tree is to use pre-order traversal. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as #.

     _9_
    /   \
   3     2
  / \   / \
 4   1  #  6
/ \ / \   / \
# # # #   # #
For example, the above binary tree can be serialized to the string "9,3,4,#,#,1,#,#,2,#,6,#,#", where # represents a null node.

Given a string of comma separated values, verify whether it is a correct preorder traversal serialization of a binary tree. Find an algorithm without reconstructing the tree.

Each comma separated value in the string must be either an integer or a character '#' representing null pointer.

You may assume that the input format is always valid, for example it could never contain two consecutive commas such as "1,,3".

Example 1:
"9,3,4,#,#,1,#,#,2,#,6,#,#"
Return true

Example 2:
"1,#"
Return false

Example 3:
"9,#,#,1"
Return false
```

```java
public class Solution {
    public boolean isValidSerialization(String preorder) {
        if(preorder == null || preorder.length() == 0) return false;
        if(preorder.length() == 1 && preorder.charAt(0) == '#') return true;
        
        String[] nodes = preorder.split(",");
        int diff = 1;
        
        for(String node : nodes){
            diff--; //processing node, so decrement for indegree
            if(diff < 0) return false; //this should never happen which means its not a proper preorder serialization
            
            if(!node.equals("#")) diff +=2; //adds two outdegrees including leaf, leaf will add two # # and non leaf will add two non null nodes or 1 non null and #
        }
        
        return diff == 0; // the diff should become 0 always
    }
}
```
