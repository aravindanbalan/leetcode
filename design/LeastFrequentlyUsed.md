Design and implement a data structure for Least Frequently Used (LFU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reaches its capacity, it should invalidate the least frequently used item before inserting a new item. For the purpose of this problem, when there is a tie (i.e., two or more keys that have the same frequency), the least recently used key would be evicted.

Follow up:
Could you do both operations in O(1) time complexity?

```java
public class LFUCache {
    
    //DLL storing count and LinkedHashSet of keys
    class Node{
        int count;
        Set<Integer> set;
        Node prev;
        Node next;
        
        public Node(int count){
            this.count = count;
            set = new LinkedHashSet<Integer>();
        }
    }
    
    int cap;
    Map<Integer, Integer> valueHash;
    Map<Integer, Node> nodeHash;
    Node head;
    
    public LFUCache(int capacity) {
        this.cap = capacity;
        valueHash = new HashMap<Integer, Integer>();
        nodeHash = new HashMap<Integer, Node>();
    }
    
    public int get(int key) {
        if(valueHash.containsKey(key)){
            increaseCount(key);
            return valueHash.get(key);
        }
        return -1;
    }
    
    public void put(int key, int value) {
        if(cap == 0) return;
        if(valueHash.containsKey(key)){
            valueHash.put(key, value);
        }else{
            //check if reached capacity 
            if(valueHash.size() >= cap){
                removeOld();  //remove less frequent (head) and first key in Head (least recently used)
            }
            valueHash.put(key, value);
            
            //add to head, creates a node with frequency count 0
            addToHead(key);
        }
        
        //increase frequency count
        increaseCount(key);
    }
    
    private void increaseCount(int key){
        Node node = nodeHash.get(key);
        node.set.remove(key);
        
        //if the next node is null, then create one with increased count
        if(node.next == null){
            node.next = new Node(node.count +1);
            node.next.set.add(key); //add it to the keys of the set
            node.next.prev = node;
        }else if(node.next.count == node.count +1){  //say after 0 we have 1
            node.next.set.add(key);
        }else{ //say after 0 we have 2
            Node nextNode = new Node(node.count +1);
            nextNode.set.add(key);
            nextNode.prev = node;
            nextNode.next = node.next;
            node.next.prev = nextNode;
            node.next = nextNode;
        }
        
        nodeHash.put(key, node.next);
        //if current node's set count becomes zero time to remove
        if(node.set.size() == 0) remove(node);
    }
    
    private void removeOld(){
        if(head == null) return;
        int old = 0;
        
        for(int n : head.set){
            old = n;
            break;
        }
        
        head.set.remove(old);
        //if nothing in head
        if(head.set.size() == 0) remove(head);
        
        nodeHash.remove(old);
        valueHash.remove(old);
    }
    
    private void addToHead(int key){
        if(head == null){
            head = new Node(0);
            head.set.add(key);
        }else if(head.count > 0){  //if head starts with count 1
            Node node = new Node(0);
            node.set.add(key);
            
            head.prev = node;
            node.next = head;
            
            head = node;
        }else{
            head.set.add(key);
        }
        
        //update node hash map
        nodeHash.put(key, head);  
    }
    
    //remove a node from DLL
    private void remove(Node node){
        if(node.prev == null){
            head = node.next;
        }else{
            node.prev.next = node.next;
        }
        
        if(node.next!=null){
            node.next.prev = node.prev;
        }
    }
}

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache obj = new LFUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```
