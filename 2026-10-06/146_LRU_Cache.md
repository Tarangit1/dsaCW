# 146. LRU Cache

### Idea
Use a doubly linked list + HashMap:
- The HashMap stores key -> node for O(1) lookup.
- The doubly linked list keeps the most recently used item at the front and the least recently used item at the tail.
- When a key is accessed or updated, move it to the front.
- When the cache is full, remove the node at the tail.

### Why this works
A cache needs fast access and eviction of the least recently used item. A doubly linked list lets us:
- insert at the front in O(1)
- remove any node in O(1)
- evict from the tail in O(1)

Together with a HashMap, every operation becomes O(1) on average.

### Java solution
```java
class LRUCache {
    private class Node {
        int key;
        int value;
        Node prev;
        Node next;

        Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    private final Map<Integer, Node> map = new HashMap<>();
    private final int capacity;
    private final Node head;
    private final Node tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.head = new Node(-1, -1);
        this.tail = new Node(-1, -1);
        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;
        }

        Node node = map.get(key);
        moveToFront(node);
        return node.value;
    }

    public void put(int key, int value) {
        if (map.containsKey(key)) {
            Node node = map.get(key);
            node.value = value;
            moveToFront(node);
            return;
        }

        if (map.size() == capacity) {
            Node lru = tail.prev;
            removeNode(lru);
            map.remove(lru.key);
        }

        Node newNode = new Node(key, value);
        addToFront(newNode);
        map.put(key, newNode);
    }

    private void addToFront(Node node) {
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
    }

    private void removeNode(Node node) {
        Node prevNode = node.prev;
        Node nextNode = node.next;
        prevNode.next = nextNode;
        nextNode.prev = prevNode;
    }

    private void moveToFront(Node node) {
        removeNode(node);
        addToFront(node);
    }
}
```

### Complexity
- Time: O(1) for get and put
- Space: O(capacity)

### Example
```java
LRUCache cache = new LRUCache(2);
cache.put(1, 1);
cache.put(2, 2);
cache.get(1);    // returns 1
cache.put(3, 3); // evicts 2
cache.get(2);    // returns -1
```
