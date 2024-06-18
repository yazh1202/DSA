
```java
class LRUCache {
    class Dnode{
        Dnode prev;
        Dnode next;
        int key;
        int val;
        Dnode(int key,int val){
            this.key = key;
            this.val = val;
            prev = null;
            next=null;
        }

    }
    HashMap<Integer,Dnode> hm = new HashMap<>();
    int size;
    Dnode head = new Dnode(-1,-1);
    Dnode tail = new Dnode(-1,-1);

    public LRUCache(int capacity) {
        size = capacity;
        head.next=tail;
        tail.prev= head;
    }
    
    public int get(int key) {
        if(hm.containsKey(key)){
            Dnode res = hm.get(key);
            int ans = res.val;
            hm.remove(key);
            removeNode(res);
            addNode(res);

            hm.put(key,head.next);
            return ans;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        if(hm.containsKey(key)){
            Dnode curr = hm.get(key);
            hm.remove(key);
            removeNode(curr);
        }
        if(hm.size()==size){
            hm.remove(tail.prev.key);
            removeNode(tail.prev);
        }
        addNode(new Dnode(key,value));
        hm.put(key,head.next);
    }

    void addNode(Dnode node){
        Dnode temp = head.next;
        
        node.next = temp; 
        node.prev = head;

        head.next = node;
        temp.prev = node;

    }
    void removeNode(Dnode node){
        Dnode prev = node.prev;
        Dnode nxt = node.next;

        prev.next = nxt;
        nxt.prev = prev;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```