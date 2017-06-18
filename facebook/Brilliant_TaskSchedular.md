```
Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks.Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given tasks.

Example 1:
Input: tasks = ['A','A','A','B','B','B'], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
```
```java
public class Solution {
    public int leastInterval(char[] tasks, int n) {
        if(tasks.length == 0) return 0;
        
        //count the characters
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        
        for(char c : tasks){
            if(map.containsKey(c)) map.put(c, map.get(c) + 1);
            else map.put(c, 1);
        }
        
        //use a max heap to store the entries of the map and pick a task which has more to complete
        PriorityQueue<Map.Entry<Character,Integer>> maxHeap = new PriorityQueue<Map.Entry<Character,Integer>>(map.size(), new Comparator<Map.Entry<Character,Integer>>(){
            @Override
            public int compare(Map.Entry<Character,Integer> a, Map.Entry<Character,Integer> b){
               return (a.getValue()!=b.getValue()) ? b.getValue() - a.getValue() : a.getKey() - b.getKey(); 
               //if values are diff pick the highest one, if same choose alphabetically
            }
        }); 
        
        maxHeap.addAll(map.entrySet()); //add all entries to maxHeap
        int count = 0;
        
        while(!maxHeap.isEmpty()){
            
            int k = n + 1; // atleast n width (since atleast n it needs to > n)
            //try to pick k tasks and execute
            
            List<Map.Entry<Character, Integer>> templist = new ArrayList<Map.Entry<Character, Integer>>();
            while(k > 0 && !maxHeap.isEmpty()){
                k--;
                count++;
                Map.Entry<Character, Integer> top = maxHeap.poll();
                top.setValue(top.getValue() - 1);  //decrement the count so that later its added to heap again
                templist.add(top);
            }
            
            for(Map.Entry<Character, Integer> entry : templist){
                if(entry.getValue() > 0) maxHeap.add(entry); //add the entry again as the task is yet to complete
            }
            
            if(maxHeap.isEmpty()) break; //if queue becomes empty, then we have executed all tasks successfully
            
            count += k; //if k > 0, then it means we need to add that much idle time as we couldnt find that many tasks (n+1).
        }
        
        return count;
    }
}
```
