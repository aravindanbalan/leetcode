Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

For example,
Given [[0, 30],[5, 10],[15, 20]],
return 2.

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public int minMeetingRooms(Interval[] intervals) {
        if(intervals == null || intervals.length == 0)
            return 0;
        if(intervals.length == 1)
            return 1;
            
        //sort based on start time
        Arrays.sort(intervals, new Comparator<Interval>(){
            @Override
            public int compare(Interval a, Interval b){
                return ((Integer) a.start).compareTo(b.start);
            }
        });
        
        PriorityQueue<Interval> minHeap = new PriorityQueue<Interval>(intervals.length, new Comparator<Interval>(){
            @Override
            public int compare(Interval a, Interval b){
                return ((Integer)a.end).compareTo(b.end);
            }
        });
        
        minHeap.offer(intervals[0]);
        
        for(int i = 1; i< intervals.length;i++){
            Interval interval = minHeap.poll();
            
            if(intervals[i].start >= interval.end){
                interval.end = intervals[i].end;
            }else{
                //it needs a new meeting room
                minHeap.offer(intervals[i]);
            }
            
            minHeap.offer(interval);
        }
        
        return minHeap.size();
    }
}
```
