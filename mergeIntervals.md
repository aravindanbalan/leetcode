```
Given a collection of intervals, merge all overlapping intervals.

For example,
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18].
```

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
    public List<Interval> merge(List<Interval> intervals) {
        if(intervals == null || intervals.size() <= 1) return intervals;
        
        //sort based on start time
        Collections.sort(intervals, new Comparator<Interval>(){
            @Override
            public int compare(Interval a, Interval b){
                return ((Integer)a.start).compareTo(b.start);
            }
        });
        
        List<Interval> result = new ArrayList<>();
        
        int start = intervals.get(0).start;
        int end = intervals.get(0).end;
        
        for(Interval interval : intervals){
            if(interval.start <= end){ //overlapping intervals
                end = Math.max(interval.end, end);
            }else{
                //first non overlapping interval
                //so add the previous one to result
                result.add(new Interval(start, end));
                //reset start and end
                start = interval.start;
                end = interval.end;
            }
        }
        
        //add the last interval
        result.add(new Interval(start, end));
        
        return result;
    }
}
```
