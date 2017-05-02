Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. 
There is no restriction on how your serialization/deserialization algorithm should work. 
You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

``` java

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Codec {

    private static final String SPLITTER = ",";
    private static final String NULL = "#";

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        //Use PreOrder to serialize the tree
        
        StringBuilder sb = new StringBuilder();
        buildString(root, sb);
        return sb.toString();
    }
    
    private void buildString(TreeNode root, StringBuilder sb){
        if(root == null){
            sb.append(NULL).append(SPLITTER);
            return;
        } 
        
        sb.append(String.valueOf(root.val)).append(SPLITTER);
        buildString(root.left, sb);
        buildString(root.right, sb);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        Deque<String> nodes = new LinkedList<String>();
        nodes.addAll(Arrays.asList(data.split(SPLITTER)));
        return buildTree(nodes);
    }
    
    private TreeNode buildTree(Deque<String> nodes){
        String node = nodes.remove();
        if(node.equals(NULL)){ 
            return null;
        }else{
            TreeNode newNode = new TreeNode(Integer.valueOf(node));
            //recursively assign left and right subtrees
            newNode.left = buildTree(nodes);
            newNode.right = buildTree(nodes);
            return newNode;
        }
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));

```
