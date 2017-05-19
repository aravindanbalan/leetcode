```

Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.

Example 1:
     0          3
     |          |
     1 --- 2    4
Given n = 5 and edges = [[0, 1], [1, 2], [3, 4]], return 2.

Example 2:
     0           4
     |           |
     1 --- 2 --- 3
Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]], return 1.


```

```java
public class Solution {
    int[] parent;
    public int countComponents(int n, int[][] edges) {
        //Idea use Union find using rank and path compression
        
        if(n == 0) return 0;
        if(edges.length == 0) return n;
        
        parent = new int[n];
        
        for(int i = 0 ;i< n; i++){
            parent[i] = i;
        }
        
        //iterate thru edges and perform union
       for(int[] edge : edges){
            int root1 = find(edge[0]);
            int root2 = find(edge[1]);
            
            if(root1!= root2){
                n--; //number of connected components is one less as we are doing union
                parent[root1] = root2;
            }
        }
        
        return n;
    }
    
    private int find(int node){
        while(parent[node]!=node){
            parent[node] = parent[parent[node]];  //path compression
            node = parent[node];
        }
        
        //if equal while ends and we return node
        return node;
    }
}
```
