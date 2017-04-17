Given two 1d vectors, implement an iterator to return their elements alternately.

For example, given two 1d vectors:

v1 = [1, 2]
v2 = [3, 4, 5, 6]
By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1, 3, 2, 4, 5, 6].

```java
public class ZigzagIterator {

    private LinkedList<Iterator> queue;
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        queue = new LinkedList<Iterator>();
          if(!v1.isEmpty()) queue.add(v1.iterator());
        if(!v2.isEmpty()) queue.add(v2.iterator());
    }

    public int next() {
        Iterator it = queue.remove();
        int result = (Integer) it.next();
        if(it.hasNext()) queue.add(it);
        
        return result;
    }

    public boolean hasNext() {
        return !queue.isEmpty();
    }
}

/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator i = new ZigzagIterator(v1, v2);
 * while (i.hasNext()) v[f()] = i.next();
 */

```
