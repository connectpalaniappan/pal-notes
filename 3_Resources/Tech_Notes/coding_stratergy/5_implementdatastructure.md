## In-built data structures
| Data structure | Java (Java methods)|
| :---        |    :----:   |
| Array/List | ArrayList (add, remove, get) | 
| LinkedList | LinkedList (add, remove, get)| 
| Hashtable | HashMap (put, remove, get)| 
| Queue | Deque (offer, poll, peek)| 
| Stack | Stack, Deque (push, pop, peek) | 
| Binary string to Integer | Integer.parseInt(binaryString, 2) | 

## Implementation tricks and techniques

### Array
* int[] is an object and can be stored in collections
```java
 final List<int[]> list = new LinkedList<>();
```

###  Linked list
  * When deleting a node, always be at the previous node.
    * previous.next = deleteNode.next
  * when inserting a node, always be at the previous node
    * newNode.next = previous.next;
    * previous.next = newNode;
    
###  Doubly linked list
  * When deleting a node, you can be at the previous node.
    * previous.next = deleteNode.next
    * deleteNode.next.prev = previous (when you maintain a dummy tail, you don't need to do null checks)
  * When adding a new node, you can be at the previous node
    * newNode.next = previous.next
    * previous.next.prev = newNode; (when you maintain a dummy head, you don't need to do null checks)
    * previous.next = newNode;
    * newNode.prev = previous;