```
There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

For example:

2, [[1,0]]
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1]

4, [[1,0],[2,0],[3,1],[3,2]]
There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is [0,1,2,3]. Another correct ordering is[0,2,1,3].
```

```java

public class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        
        if(numCourses == 0) return new int[0];
        if(numCourses == 1) return new int[]{0};
        
        List<Integer> result = new LinkedList<Integer>();

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
            //should be in reverse order
            result.add(0, course);
            
            List<Integer> dependentCourses = graph[course];
            
            for(int dependentCourse : dependentCourses){
                indegree[dependentCourse]--;
                if(indegree[dependentCourse] == 0){
                    count++;
                    queue.add(dependentCourse);
                }
            }
        }
        
        //only if we can finish all courses return the solution
        if(count == numCourses){
            int[] resultArray = new int[result.size()]; 
            int i = 0;
            for(int course : result){
                resultArray[i++] = course;
            }
            return resultArray;
        }
    
        return new int[0];
    }
}
```
