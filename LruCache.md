```
Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

Follow up:
Could you do both operations in O(1) time complexity?


```

```java
public class LRUCache {
    class Node{
        int key;
        int val;
        Node next;
        Node pre;
        
        public Node(int key, int value){
            this.key = key;
            this.val = value;
        }
    }
    
    private Map<Integer, Node> map;
    private int capacity;
    private Node head; //add to head the most recently used item
    private Node end; //to remove the least recently used node

    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<Integer, Node>();
    }
    
    public int get(int key) {
        if(map.containsKey(key)){
            Node node = map.get(key);
            remove(node);
            setHead(node);
            return node.val;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        if(map.containsKey(key)){
            Node old = map.get(key);
            old.val = value;
            remove(old);
            setHead(old);
        }else {
            Node node = new Node(key, value);
            
            //check if the cache has reached capacity, if yes remvoe the tail from DLL and hashmap
            if(map.size() >=capacity){
                map.remove(end.key);
                remove(end);    
               setHead(node);
            }else {
                setHead(node);
            }
            
            map.put(key, node);
        }
    }
    
    private void remove(Node node){
        if(node.pre!=null){
            node.pre.next = node.next;
        }else{
            head = node.next;
        }
        
        if(node.next!=null){
            node.next.pre = node.pre;
        }else{
            end = node.pre;
        }
    }
    
    private void setHead(Node node){
        node.next = head;
        node.pre = null;
        
        if(head!=null){
            head.pre = node;
        }
        
        head = node;
        
        if(end == null){
            end = node;
        }
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```
