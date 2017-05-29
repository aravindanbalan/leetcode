```
There are N students in a class. Some of them are friends, while some are not. Their friendship is transitive in nature. For example, if A is a direct friend of B, and B is a direct friend of C, then A is an indirect friend of C. And we defined a friend circle is a group of students who are direct or indirect friends.

Given a N*N matrix M representing the friend relationship between students in the class. If M[i][j] = 1, then the ith and jth students are direct friends with each other, otherwise not. And you have to output the total number of friend circles among all the students.

Example 1:
Input: 
[[1,1,0],
 [1,1,0],
 [0,0,1]]
Output: 2
Explanation:The 0th and 1st students are direct friends, so they are in a friend circle. 
The 2nd student himself is in a friend circle. So return 2.
```

```java
public class Solution {
    int[] parent;
    int[] rank;
    int count;
    public int findCircleNum(int[][] M) {
        int n = M.length;
        if(n <= 1) return 1; //no friends or just one guy
        
        //use union find.
        //idea : first convert the relationship between friends into edges array
        parent  = new int[n];
        rank = new int[n];
        
        for(int i = 0; i< n ;i++){
            parent[i] = i; //they are in the same set
        }
        
        count = n;
        for(int i = 0; i< n-1;i++){
            for(int j = i+1 ; j<n ;j++){
                if(M[i][j] == 1){ //if they are friends
                
                    //Union by rank to make union and find on O(Logn)
                    union(i, j);
                }
            }
        }
        
        return count;
        //Overall time complexity : O(n2Log(n))
        //overall space : O(n) - parent and rank array
        
        //BFS or DFS would be O(n2) time and O(n) space (queue or recursion stack)
    }
    
    //O(logn) - complexity
    private void union(int node1, int node2){
        int parent1 = find(node1);
        int parent2 = find(node2);
        
        if(parent1 == parent2) return;
        
        if(rank[parent2]  > rank[parent1]){
            parent[parent1] = parent2;
        }else{
            if(rank[parent1] == rank[parent2]){
                rank[parent1]++;
            }
            parent[parent2] = parent1;
        }
        count--;
    }
    
    //O(logn) - as worst case it takes < O(logn) with path compression as first time its O(logn) and next time its constant.
    //O(n) - without path compression
    private int find(int node){
        while(parent[node]!=node){
            parent[node] = parent[parent[node]]; //path compression
            node = parent[node];
        }
        return node;
    }
    
    
    //You can also do DFS - connected components 
    //Time O(n2)
    //space - O(n)
    
    // public void dfs(int[][] M, boolean[] visited, int i) {
    //     for (int j = 0; j < M.length; j++) {
    //         if (M[i][j] == 1 && !visited[j]) {
    //             visited[j] = true;
    //             dfs(M, visited, j);
    //         }
    //     }
    // }
    // public int findCircleNum(int[][] M) {
    //     boolean[] visited = new boolean[M.length];
    //     int count = 0;
    //     for (int i = 0; i < M.length; i++) {
    //         if (!visited[i]) {
    //             dfs(M, visited, i);
    //             count++;
    //         }
    //     }
    //     return count;
    // }
}
```
