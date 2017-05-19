```
Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

For example:

Given n = 5 and edges = [[0, 1], [0, 2], [0, 3], [1, 4]], return true.

Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]], return false.

Note: you can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.
``

```java
public class Solution {
    int[] parent;
    public boolean validTree(int n, int[][] edges) {
        
        if(n <= 1) return true;
        if(edges.length == 0) return false;
        
        parent = new int[n];
        
        for(int i = 0; i< n ; i++){
            //set parent to itself initially
            parent[i] = i;
        }
        
        //Tree cannot have a cycle, detect cycle
        for(int[] edge : edges){
            int x = find(edge[0]);
            int y = find(edge[1]);
            
            if(x == y) //then cycle
                return false;
                
            //else do union
            parent[x] = y;
        }
        
        //there are only n-1 edges in a tree;
        return edges.length == n-1;
    }
    
    private int find(int node){
        while(parent[node]!=node){
           parent[node] = parent[parent[node]]; //path compression 
           node = parent[node];
        }
        return node;
    }
}
```
