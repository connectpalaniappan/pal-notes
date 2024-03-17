## Datastructures

Method to store information

1. [Array](#arraysarraylist)
   1. [Two dimensional array](#two-dimensional-array) 
   2. [Circular Array](#circular-array)
2. [LinkedList](#linkedlist)
   1. [Doubly Linked List](#doubly-linked-list)
   2. [Circular Linked List](#circular-linked-list)
3. [String](#strings)
4. [Search - Hashtables](#hashtables)
   1. [HashMap](#hashmap) 
   2. [TreeMap](#treemap) 
   3. [LinkedHashMap](#linkedHashMap) 
   4. [HashSet](#hashset) 
   5. [TreeSet](#treeset) 
5. [Queue](#queue) 
   1. [Circular queue](#circular-queue)
6. [Stack](#stack)
7. [Tree](#tree)
   1. [Binary Tree](#binary-tree)
   2. [N-ary Tree](#)
   3. [Tries](#tries)
8. [Search - Binary search tree](#binary-search-tree)
   1. [Search - Red-Black Binary search tree](#red-black)
9. [Sort - Heap/Priority Queue](#priority-queue-minmax-heap) - Sorted, Duplicate allowed
10. [Graphs](#graphs)
11. [Disjoint set](#disjoint-set) 
12. [Spanning Tree](#spanning-tree)
13. [AVL](#avl)
14. [Segment Tree](#segment-tree)
15. [Bit operations](#bit-operations)

### Arrays/ArrayList
* Description
  * An array is a basic data structure to store a collection of elements sequentially
  * Elements can be accessed randomly since each element in the array can be identified by an array index.
* Use case
  * Need to access an element by index often, an array might be a better choice than a linked list.
  * faster index lookups
  * Adjacent memory locations
  * Similar data
* Functions
  * length: total number of elements in the array (capacity)
  * size: populated elements in the array. Need to be tracked explicitly.
* Implementation
  * Java
    * fixed array: new int[]
      * `int[] a0 = new int[5];  int[] a1 = {1, 2, 3};`
    * variable array: interface - List, implementation - ArrayList
      * `List<Integer> v0 = new ArrayList<>(); v1 = new ArrayList<>(Arrays.asList(a));`
    * Sort operation: Arrays.sort(arr)
    * Fill operation: Arrays.fill(arr, 0)
  * C++ 
    * variable array: vector

### Two-dimensional array
* Description
  * a two-dimensional array also consists of a sequence of elements.
  * elements can be laid out in a rectangular grid rather than a line.
* Implementation
  * Java
    * two-dimensional array is actually a one-dimensional array which contains M elements, each of which is an array of N integers.
  * C++
    * C++ stores the two-dimensional array as a one-dimensional array.
    * actually A[i][j] equals to A[i * N + j] if we defined A as a one-dimensional array which also contains M * N elements.

### Circular Array
* Description
* Use case
  * Cyclic in nature
  * Efficiency in space utilization
* Time complexity
* Space complexity
* Implementation
  * Java

### Linkedlist
* Description
  * Each node in a singly-linked list contains not only the value but also a reference field to link to the next node. 
  * By this way, the singly-linked list organizes all the nodes in a sequence.
  * Not able to access the data at a random position in constant time.
* Use case
  * need to add or delete a node frequently, a linked list could be a good choice.
  * Maintain insertion order
  * Data needs to be inserted or deleted frequently
  * Data stored in random memory locations and linked together by reference fields.
  * Better in reusing memory.
* Implementation
  * Java - LinkedList class

### Doubly linked list
* Use case
  * A node in a double linked list has 
    * the value field, 
    * "next" reference field to know the next node.
    * "prev" reference field to know the previous node.
* Implementation
  * Java

### Circular Linked List
* Use case
  * Cyclic in nature
  * Similar to double linked list.
* Time complexity
* Space complexity
* Implementation
  * Java

### Strings
* Description
  * String is actually an array of unicode characters. 
  * Perform almost all the operations we used in an array.
  * Mutability
    * Immutable means that you can't change the content of the string once it's initialized.
      * If you want to modify just one of the characters, you have to create a new string.
    * In java, string is immutable
      * To make it mutable, convert string to char array.
      * Use other data structures such as StringBuilder.
    * In C++, string is mutable
* Use case
* Time complexity
  * finding operation: O(N)
  * substring operation: O(N)
  * Concatenate operation: O(N^2)
    * In Java, concatenation works by first allocating enough space for the new string, copy the contents from the old string and append to the new string.
    * Using StringBuilder, the time complexity is O(N)
* Functions
  * compare function
    * Java: may not use "==" to compare two strings. 
      * When we use "==", it actually compares whether these two objects are the same object.
    * C++: May use "==" to compare two strings.
* Implementation
  * Java
      * Implementation: String
    
### Hashtables
* Description
  * Hash Table is a data structure which organizes data using hash functions in order to support quick insertion and search.
  * By choosing a proper hash function, the hash table can achieve wonderful performance in both insertion and search.
  * Can be classified into hashmap or hashset.
  * Hash function
    * Important component of a hash table which is used to map the key to a specific bucket.
    * Hash function will depend on the range of key values and the number of buckets
    * Assign the key to the bucket as uniformly as you can
    * Perfect hash function will be a one-one mapping between the key and the bucket.
    * In most cases, a hash function is not perfect and it is a tradeoff between the amount of buckets and the capacity of a bucket.
    * In most cases, collisions is unavoidable. Here are collision resolution questions?
      * How to organize the values in the same bucket?
      * What if too many values are assigned to the same bucket?
      * How to search for a target value in a specific bucket?
      * Resolution solutions:
      * questions are related to the capacity of the bucket and the number of keys which might be mapped into the same bucket according to our hash function
      * Typically, if N is constant and small, we can simply use an array to store keys in the same bucket. 
      * If N is variable or large, we might need to use height-balanced binary search tree instead.
* Implementation
  * Java

### HashMap
* Description
  * hash map is one of the implementations of a map data structure to store (key, value) pairs.
* Use case
  * grouping information by key e.g. anagrams
  * aggregate all the information by key

### TreeMap

### LinkedHashMap

### Hashset
* Description
  * hash set is one of the implementations of a set data structure to store no repeated values.
* Use case
  * Duplicate check
  * Unique check

### TreeSet
* Description
  * Internally 
* Function
  * 
* Implementation
  * TreeSet class - Internal implementation: Binary search tree

### Queue
* Use case  
  * Processing order - First in first order
  * Ideal for breath first solutions
* Functions
  * The insert operation is also called enqueue and the new element is always added at the end of the queue.
  * The delete operation is called dequeue. You are only allowed to remove the first element.
* Implementation
  * Java

### Circular Queue
* Use case
  * Cyclic in nature
  * A more efficient way is to use a circular queue. Specifically, we may use a fixed-size array and two pointers to indicate the starting position and the ending position. 
  * And the goal is to reuse the wasted storage we mentioned previously.
* Time complexity
* Space complexity
* Implementation
  * Java

### Stack
* Use case  
  * Processing order - Last in first out
  * Process expressions 
  * infer something from past (push elements left to right array traversal) or future data (push elements right to left array traversal)
  * Ideal for depth first solutions - Iterative approach - Alternative for recursive solutions
* Functions
  * push
  * pop
  * peek
* Implementation
    * Java
      * Stack class

### Tree
* Description
  * Tree is an directed graph in which any two vertices are connected by exactly one path. 
    * In other words, any connected directed graph without cycles is a tree.
* Use case  
  * Hierarchical structure
* Functions
* Implementation
    * Java

### Binary tree
* Definition
  * Binary Tree: Tree data structure in which each node has at most two children, 
    * which are referred to as the left child and the right child.
  * Complete Binary Tree: 
  * Height of a binary tree: O(log N) where n is the total number of elements
* Functions
* Implementation
  * Java

### N-ary Tree
* Definition
  * N-ary Tree: Tree node has multiple children.
* Functions
* Implementation
  * Java

### Tries
* Description
  * Trie, also called prefix tree, is a special form of a Nary tree.
  * Typically, a trie is used to store strings. 
    * Each Trie node represents a string (a prefix). 
    * Each node might have several children nodes while the paths to different children nodes represent different characters. 
    * And the strings the child nodes represent will be the origin string represented by the node itself plus the character on the path.
  * Root node is associated with the empty string.
  * Might declare a boolean in each node as a flag to indicate if the string represented by this node is a word or not.
  * Why is it called a prefix tree?
    * Important property of Trie is that all the descendants of a node have a common prefix of the string associated with that node. 
  * Representation
    * Array
      * If we store strings which only contains letter a to z, we can declare an array whose size is 26 in each node to store its children nodes. 
      * And for a specific character c, we can use c - 'a' as the index to find the corresponding child node in the array.
      * Fast to visit a child node.
      * Easy to visit a specific child since we can easily transfer a character to an index in most cases.
      * Not all children nodes are needed. So there might be some waste of space.
    * Map
      * Use a hashmap to store children nodes.
      * Key of the hashmap are characters and the value is the corresponding child node.
      * Easier to visit a specific child directly by the corresponding character. But it might be a little slower than using an array.
      * Saves some space since we only store the children nodes we need. 
      * More flexible because we are not limited by a fixed length and fixed range.
* Use case
  * Identify words in a dictionary.
  * Autocomplete
  * Spell checker
* Function
  * Insertion
  * Search for a prefix
  * Search for a valid word
* Implementation
  * Java

### Binary search tree
* Description
  * Value in each node 
    * greater than (or equal to) any values in its left subtree 
    * less than (or equal to) any values in its right subtree.
  * fetch numbers in non-increasing order using in-order traversal
  * Where to add a child node 
    * Depend on the relationship between the value of the node and the target value
* Use case
  * store data in order and need several operations, such as search, insertion or deletion, at the same time, a BST might be a good choice.
* Function
  * Search in BST
    * search the left or right subtrees according to the relation of the value of the node and the value of our target node;
    * repeat STEP 1 until reaching an external node;
  * Insert in BST
    * search the left or right subtrees according to the relation of the value of the node and the value of our target node; 
    * repeat STEP 1 until reaching an external node; 
    * add the new node as its left or right child depending on the relation of the value of the node and the value of our target node.
  * Delete in BST
    * If the target node has no child, we can simply remove the node. 
    * If the target node has one child, we can use its child to replace itself. 
    * If the target node has two children, replace the node with its in-order successor or predecessor node and delete that node.
* Implementation
  * Java

### Priority Queue (Min/Max heap)
* Definition
  * a Heap is a special type of binary tree. 
  * Heap property: A heap is a binary tree that meets the following criteria:
    * Is a complete binary tree; 
    * The value of each node must be no greater than (or no less than) the value of its child nodes.
  * A priority queue is an abstract data type, while a Heap is a data structure. 
    * a Heap is not a Priority Queue, but a way to implement a Priority Queue.
    * List and arrays can be used to implement a priority queue
  * Max Heap: Each node in the Heap has a value no less than its child nodes. 
    * Therefore, the top element (root node) has the largest value in the Heap.
  * Min Heap: Each node in the Heap has a value no larger than its child nodes. 
    * Therefore, the top element (root node) has the smallest value in the Heap.
* Algorithm
  * Heapify after inserting an node
    * Insertion means adding an element to the Heap. 
    * After inserting the element, the properties of the Heap should remain unchanged.
    * Add the node to the end of the binary tree to make a complete binary tree
    * compare the added node with the parent, depending on whether it is max or min heap,
      * swap the parent value with the added value.
    * Continue the above step until the root of the tree.
  * Heapify after deleting an node
    * Deletion means removing the “top” element from the Heap. 
    * After deleting the element, the property of Heap should remain unchanged.
    * Delete the last node and set the value of the last node as the root value.
    * Identify the child which does not satisfy the heap property.
      * Continue swapping the child and the parent node value until the heap property is satisfied.
* Techniques
  * Root node with have the index 1 in the array data structure
  * Parent for node n will be at n/2
  * Child for node n will be at n*2 and n*2+1
  * Check whether n is a leaf node, node index value i should be greater than (total elements/2)
* Use case
  * top k problem
    * Time complexity: O(K logN + N) or O(N logK)
    * Space complexity: O(N) or O(K)
  * k-th largest/smallest element
    * Time complexity: O(K logN + N) or O(NlogK)
    * Space complexity: O(N) or O(K)
  * Heap sorting 
    * Time complexity: O(N logN)
    * Space complexity: O(N)
* Functions
  * `Add` add to a new element to the heap
  * `peek` look at the top element
  * `poll` remove the top element
  * `size` size of the heap
* Implementation
  * Java
    * PriorityQueue class to create a min heap by default
    * `new PriorityQueue<>(Collections.reverseOrder())` would create a max heap 
  * Python
    * `Heapq` can be used to construct a min heap
    * there is no max heap implementation in priority queue
    * You can implement a max heap by multiplying all the numbers with -1 before adding to the priority queue.

### Graphs
* Define
  * Graph: non-linear data structure consisting of vertices and edges.
  * Vertices: are nodes or vertex or points in the graph
  * Edge: The connection between two vertices are the edges of the graph.
  * Path: the sequence of vertices to go through from one vertex to another.
  * Path Length: the number of edges in a path.
  * Cycle: a path where the starting point and endpoint are the same vertex.
  * Negative Weight Cycle: In a “weighted graph”, if the sum of the weights of all edges of a cycle is a negative value
  * Connectivity: if there exists at least one path between two vertices, these two vertices are connected.
  * Degree of a Vertex: the term “degree” applies to unweighted graphs. The degree of a vertex is the number of edges connecting the vertex.
  * In-Degree: “in-degree” is a concept in directed graphs. Number of edges to the vertex.
  * Out-Degree: “out-degree” is a concept in directed graphs. Number of edges from the vertex. 
* Types
  * Undirected graphs - edges between any two vertices in an “undirected graph” do not have a direction, indicating a two-way relationship.
  * directed graphs - edges between any two vertices in a “directed graph” graph are directional.
  * Weighted graph - Each edge in a “weighted graph” has an associated weight. The weight can be of any metric, such as time, distance, size, etc.
* Use case
* Functions
* Implementation
    * Java

### Spanning Tree
* Define
  * connected subgraph in an undirected graph 
    * all vertices are connected with the minimum number of edges
  * Undirected graph can have multiple spanning trees.
  * `Minimum spanning tree`: spanning tree with the minimum possible total edge weight in a “weighted undirected graph”.
  * `cut` is a partition of vertices in a graph into two disjoint subsets.
    * For any cut C of the graph, if the weight of an edge E in the cut-set of C is strictly smaller than the weights of all other edges of the cut-set of C, then this edge belongs to all MSTs of the graph.
  * `crossing edge` is an edge that connects a vertex in one set with a vertex in the other set.
* Use case
* Implementation
  * Java

### Disjoint set
* Use case
  * address the connectivity between the components of a network.
  * two people share a common ancestor.
* Functions
  * The find function finds the root node of a given vertex.
  * The union function unions two vertices and makes their root nodes the same.
  * The connected function makes use of the find function to see whether the vertexes are connected or not.
* Implementation
  * Java

### AVL
* Use case
* Time complexity
* Space complexity
* Implementation
    * Java

### Red black
* Use case
* Time complexity
* Space complexity
* Implementation
    * Java
  
### Segment tree
* Use case
* Time complexity
* Space complexity
* Implementation
    * Java

### Bit operations
* Left shift (<<)
  * left shift the number by a bit
  * Use case: When you need to multiply by 10.
* Or operator (|)
  * Use case: Add two numbers
 