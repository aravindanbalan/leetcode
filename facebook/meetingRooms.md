Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

For example,
Given [[0, 30],[5, 10],[15, 20]],
return false.

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
    public boolean canAttendMeetings(Interval[] intervals) {
        
        //if empty calendar or just one meeting then he can attend
        if(intervals == null || intervals.length <= 1) return true;    
    
        int n = intervals.length;
        
        //sort based on start times
        Arrays.sort(intervals, new Comparator<Interval>(){
            @Override
            public int compare(Interval a, Interval b){
                return ((Integer)a.start).compareTo(b.start);
            }
        });
        
        int end = intervals[0].end;
        
        for(int i=1;i< n;i++){
            if(intervals[i].start < end){
                //overlapping meetings
               return false; 
            } else{
                end = intervals[i].end;
            }
        }
        
        return true;
    }
}
```
