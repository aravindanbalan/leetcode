```
There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

For example:

2, [[1,0]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

2, [[1,0],[0,1]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```

```java

public class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if(numCourses <= 1) return true;
        
        //http://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/
        //Indegree based Topological sorting 
        
        //use indegree of vertices 
        ArrayList[] graph = new ArrayList[numCourses]; 
        int[] indegree = new int[numCourses];
        
        for(int i=0;i<numCourses;i++)
            graph[i] = new ArrayList();
        
        for(int i = 0 ; i< prerequisites.length ;i++){
            indegree[prerequisites[i][1]]++;
            graph[prerequisites[i][0]].add(prerequisites[i][1]);
        }
        
        /**
         * If non of the indegree is zero, then its not a DAG, as a DAG always has atleast one vertex with indegree zero
         * If not then there is no topological sorting
         */
        int count = 0;
        Queue<Integer> queue = new LinkedList<Integer>();
        for(int i = 0 ;i < numCourses; i++){
            //which means there is no pre-requisite for this ith course
            if(indegree[i] == 0){
                queue.add(i);
                count++;
            }
        }
        
        while(!queue.isEmpty()){
            int course = queue.poll();
            
            List<Integer> dependentCourses = graph[course];
            
            for(int dependentCourse : dependentCourses){
                indegree[dependentCourse]--;
                if(indegree[dependentCourse] == 0){
                    count++;
                    queue.add(dependentCourse);
                }
            }
        }
        
       return (count == numCourses);
    }
}
```
