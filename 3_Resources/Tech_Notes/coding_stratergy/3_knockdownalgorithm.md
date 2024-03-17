
## Design patterns

1. [One pointer for Linear traversal](#one-pointer-for-linear-traversal)
2. [Two pointers for in-place operations](#two-pointers-for-in-place-operations)
3. [Binary Search](#binary-search)
4. [Cyclic sort](#cyclic-sort)
5. [Sliding Window](#sliding-window)
6. [Greedy](#greedy)
7. [Merge Interval](#merge-interval)
8. [Fast and slow pointers](#fast-and-slow-pointer)
   1. [Floyd's Algorithm](#floyds-algorithm)
9. [In place reversal of linked list](#in-place-reversal-of-linked-list)
10. [Process elements in order using Queue](#process-elements-in-order-using-queue)
11. [Infer data from past or future using Stack](#infer-from-past-or-future-data-using-stack)
12. [Key search using hashtable](#key-search-using-hashtable)
13. [Find duplicates using hashtable](#find-duplicates-using-hashtable)
14. [Group data by key using hashtable](#aggregate-information-by-key-using-hashtable)
15. [Tree In order](#tree-in-order-left-parent-right)
16. [Tree Pre order](#tree-pre-order-parent-left-right)
17. [Tree Post order](#tree-post-order-left-right-parent)
18. [Tree level order](#tree-level-order)
19. [Recursive](#recursive)
20. [Heap sort](#heap-sort)
21. [Top K problem using heap](#top-k-problem-using-heap)
22. [kth largest/smallest using heap](#kth-largestsmallest-element-using-heap)
23. [Breath first solution](#breath-first-solution-bfs)
24. [Depth first solution](#depth-first-solution-dfs)
25. [Backtracking](#backtracking)
26. [Topological sort](#topological-sort)
27. [Dynamic Programming](#dynamic-programming)
28. [Knapsack](#knapsack)
29. [Bit Manipulation](#bit-manipulation)
30. [Quick sort](#quick-sort)
31. [Merge sort](#merge-sort)
32. [Radix sort](#radix-sort)
33. [Tim sort](#tim-sort)
34. [Disjoint Set - Quick Union](#disjoint-set---quick-union)
35. [Disjoint Set - Quick find](#disjoint-set---quick-find)
36. [Graph - Prim]()
37. [Graph - Kruskal]()
38. [Graph - Dijkstra]()
39. [String - KMP]()
40. [String - Regular expressions]()
41. [String - TST]()
42. [String - Huffmann]()
43. [String - LZW]()
44. [B-Tree]()
45. [Tree - Suffix array]()
46. [Tree - maxflow]()

### One pointer for linear traversal
* Description
  * Number - positive or negative or zero or one
  * Double or single pass
* How to identify ?
* Examples

### Two pointers for in-place operations
* Description
  * inserting the array would be easier when you start on the right side for shifting elements.
  * deleting an element, would be easier when you start on the left side for shifting elements.
  * searching an element, start either left or right side
* How to identify
  * Feature problems where you deal with sorted arrays (or Linked Lists)
  * Need to find a set of elements that fulfill certain constraints
  * Set of elements in the array is a pair, a triplet, or even a subarray
  * Use when you don't need the original array for further processing.
* Examples
  * Reverse the elements in an array.
  * Squaring a sorted array (easy)
  * Triplets that sum to zero (medium)
  * Comparing strings that contain backspaces (medium)
  * Given an array and a value, remove all instances of that value in-place and return the new length.

### Binary search
* Description
  * Used to search for a value in sorted data
  * Terminologies
    * Target: the value that you are searching for
    * Index: the current location that you are searching
    * Left, Right: the indexes from which we use to maintain our search Space
    * Mid: the index that we use to apply a condition to determine if we should search left or right
    * Search space: Binary Search operates on a contiguous sequence with a specified left and right index.
  * Algorithm
    * Binary Search maintains the left, right, and middle indexes of the search space and compares the search target or 
      * applies the search condition to the middle value of the collection; 
    * if the condition is unsatisfied or values unequal, the half in which the target cannot lie is eliminated and the search continues on the remaining half until it is successful. 
    * If the search ends with an empty half, the condition cannot be fulfilled and target is not found.
  * Stages
    * Pre-processing - Sort if collection is unsorted.
    * Binary Search - Using a loop or recursion to divide search space in half after each comparison.
    * Post-processing - Determine viable candidates in the remaining space.
  * Variations
    * Template #1 (left <= right)
      * Most basic and elementary form of Binary Search 
      * **Search Condition can be determined without comparing to the element's neighbors (or use specific elements around it)**
      * No post-processing required because at each step, you are checking to see if the element has been found. 
      * If you reach the end, then you know the element is not found
      * Distinguishing syntax
        * Initial Condition: left = 0, right = length-1 
        * Termination: left > right 
        * Searching Left: right = mid-1 
        * Searching Right: left = mid+1
    * Template #2 (left < right):
      * An advanced way to implement Binary Search. 
      * Search Condition needs to access the element's immediate right neighbor 
      * **Use the element's right neighbor to determine if the condition is met and decide whether to go left or right**
      * Guarantees Search Space is at least 2 in size at each step 
      * Post-processing required. Loop/Recursion ends when you have 1 element left. 
      * Need to assess if the remaining element meets the condition.
      * Distinguishing syntax
        * Initial Condition: left = 0, right = length 
        * Termination: left == right 
        * Searching Left: right = mid 
        * Searching Right: left = mid+1
    * Template #3 (left + 1 < right)
      * An alternative way to implement Binary Search 
      * Search Condition needs to access element's immediate left and right neighbors 
      * **Use element's neighbors to determine if the condition is met and decide whether to go left or right**
      * Guarantees Search Space is at least 3 in size at each step
      * Post-processing required. Loop/Recursion ends when you have 2 elements left. 
      * Need to assess if the remaining elements meet the condition.
      * Distinguishing Syntax:
        * Initial Condition: left = 0, right = length-1 
        * Termination: left + 1 == right
        * Searching Left: right = mid 
        * Searching Right: left = mid
    * Template #4 (Binary Search With 2 Arrays)
      * Need to compare values from 2 arrays to determine our search space.
* How to identify the problem
  * search in sorted array, linked list, or matrix
  * Every time you need to search for an index or element in a collection.
* Time Complexity: O(log N)
* Space complexity: O(N)
* Examples
  * Order-agnostic Binary Search (easy)
  * Search in a Sorted Infinite Array (medium) - use template #1
  * Sqrt(x) - use template #1
  * search in a rotated sorted array - use template #1
  * First bad version - use template #2
  * Find peak element - use template #2
  * Find minimum in rotated array - use template #2
  * Search for a range - use template #3
  * Find K closest elements - use template #3

### Cyclic sort
* Description
  * iterates over the array one number at a time, and
    * if the current number you are iterating is not at the correct index,
    * you swap it with the number at its correct index.
  * iterate over the array again
    * find any invalid number (number not matching the index)
* How do I identify this pattern?
  * problems involving a sorted array with numbers in a given range
  * problem asks you to find the **missing/duplicate/smallest number** in an **sorted/rotated array**
* Examples
  * Find the Missing Number (easy)
  * Find the Smallest Missing Positive Number (medium)

### Sliding window 
* How to identify ?
  * **Min, max, longest, shortest, contained** in a **sub-sequence or sub-array**
  * Things we iterate sequentially. Focus on contiguous sequence of elements
  * The problem input is a linear data structure such as a linked list, array, or string
* Examples
  * Fixed length 
    * Maximum sum subarray of size ‘K’ (easy)
  * dynamic window size
    * Smallest subarray with sum greater than x.
  * dynamic window size with auxillary data structure
    * Longest substring with ‘K’ distinct characters (medium)
    * String anagrams (hard)
* Resource:
  * https://youtu.be/MK-NZ4hN7rs

### Greedy
* Description
  * Greedy algorithm is a simple, intuitive algorithm that is used in optimization problems.
  * Algorithm makes the optimal choice at each step as it attempts to find the overall optimal way to solve the entire problem.
  * Brute force solution is to traverse the array in two loops to identify the solution.
  * Single-pass solution
    * Find the optimal choice as you loop through the array.
    * Use the optimal choice to solve the problem.
* How to identify?
  * Find the best optimal choice for the problem.
* Examples
  * Gas station i.e. find the best starting station to complete the trip
  * Can place flowers i.e. find the ideal way to place multiple flowers

### Merge interval
* Description
  * Six overlap conditons
    * 'a' and 'b' do not overlap
    * 'a' and 'b' overlap, 'b' ends after 'a'
    * 'a' completely overlaps 'b'
    * 'a' and 'b' overlap, 'a' ends after 'b'
    * 'b' completely overlaps 'a'
    * 'b' and 'a' do not overlap
* How to identify?
  * produce a mutually exclusive intervals
  * **overlapping intervals**
* Examples
  * Intervals Intersection (medium)
  * Maximum CPU Load (hard)
    
### Fast and slow pointer
* Description
  * Traverse to k-th node from last: have two pointers:
  * one traverse to kth,
  * start second pointer from head until first reaches end.
* How to identify?
  * **cyclic linked lists or arrays**.
  * When you need to know the position of a certain element or the overall length of the linked list.
* Examples
  * Linked List Cycle (easy)
  * Palindrome Linked List (medium)
  * Cycle in a Circular Array (hard)

### Floyd's Algorithm
* Description
  * Floyd's algorithm is separated into two distinct phases. 
  * In the first phase, it determines whether a cycle is present in the list. 
    * If no cycle is present, it returns null immediately, as it is impossible to find the entrance to a nonexistant cycle. 
  * Otherwise, it uses the located "intersection node" to find the entrance to the cycle.
* How to identify?
* Example
  * Find the node where a cycle for linked list begins.

### In-place reversal of linked list
* Description
  * pattern reverses one node at a time starting with one variable (current) pointing to the head of the linked list, 
  * one variable (previous) will point to the previous node that you have processed. 
  * In a lock-step manner, you will reverse the current node by pointing it to the previous before moving on to the next node.
  * Also, you will update the variable “previous” to always point to the previous node that you have processed.
  * Change the pointer for the data to make sense e.g. palindrome
    * Change the pointer to even retain the same pointers for simplifying the flow.
* How to identify?
  * Asked to reverse a linked list without using extra memory
* Example
  * Reverse a Sub-list (medium)
  * Reverse every K-element Sub-list (medium)
* Complexity
  * Time complexity: O(N)
  * Space complexity: O(1)

### Process elements in order using queue
* Description
  * Define the queue size
  * Process elements in the order they arrive
* How to identify?
  * process in insertion order
* Example
  * Moving average
  * process stream of data

### Infer from past or future data using Stack
* Description
  * **stack** can be used to process **past/previous/last data** to infer something e.g. bracket matching
  * to process future data (reverse the input to process past data) to infer something e.g. high stock price
* How to identify?
* Example

### Key search using hashtable
* Description
  * Convert similar elements to a common key.
  * Search for keys using hashtable
* How to identify
  * Key exists or not
  * Count the occurrence of a key 
* Example

### Find duplicates using hashtable
* Description
  * Try to convert the given element into a key
    * All values belong to the same group will be mapped in the same group.
    * Values which needed to be separated into different groups will not be mapped into the same group.
  * Use hashmap to check for duplicate key
* How to identify
  * **Unique** or **Duplicate**
  * Common interest
  * Group elements based on a key
    * Duplicate structure in tree by serializing tree to a string
    * Sudoku, combine row index and column index to identify key
    * Index offset as key
* Example
  * Contains duplicate
  * Isomorphic strings
  * Group Anagrams
  * Valid sudoku

### Aggregate information by key using hashtable
* Description
  * Aggregate all the information by key
* How to identify
  * Last index occurrence of a key
  * Merge all the matrix values diagonally
* Example
  * First unique character in a string
  
### Tree In-order (left, parent, right)
* Description
  * Depth-first search
  * Binary Tree: 
    * Traverse the left subtree, 
    * then visit the root node and 
    * finally traverse the right subtree.
  * N-ary Tree: Does not make sense.
* How to identify?
  * **Binary search tree** - fetch nodes in increasing order
    * Variation can be used to fetch nodes in non-increasing order
* Examples

### Tree Pre-order (parent, left, right)
* Description
  * Depth-first search
  * Binary Tree
    * Visit the root node, 
    * then traverse the left subtree and 
    * finally traverse the right subtree.
  * N-ary Tree
    * visit the root node first and 
    * then traverse the subtree rooted at its children one by one.
* How to identify?
  * **Top-downs approach** i.e. based on the parent, compute the value for left and right subtree.
* Examples
  * Maximum depth of a tree - Need a global variable to store computations
  * Copy the tree

### Tree Post-order (left, right, parent)
* Description
  * Depth-first search
  * Binary Tree
    * Traverse the left subtree, 
    * then traverse the right subtree and 
    * finally visit the root node.
  * N-ary Tree
    * traverse the subtree rooted at its children first and 
    * then visit the root node itself.
* How to identify?
  * **Bottoms-up approach** i.e. based on the left and right node, we can make computations for parent.
* Examples
  * Maximum depth of a tree - you can return the computations at every stage
  * Delete the tree
  * Parse a post-order expression

### Tree Level-order
* Description
  * Breadth-first search
* Examples
  * Binary Tree Level Order Traversal (easy)
  * Zigzag Traversal (medium)

### Recursive
* Description
  * A simple base case (or cases) — a terminating scenario that does not use recursion to produce an answer.
  * A set of rules, also known as recurrence relation that reduces all other cases towards the base case.
  * Approach 
    * Top-Down Approach
      * In each recursive call, we will visit the node first to come up with some values, and 
        * pass these values to its children when calling the function recursively.
      * Much easier to track the result in a global variable.
      ```java 
        return specific value for null node
        update the answer if needed                              // answer <-- params
        for each child node root.children[k]:
            ans[k] = top_down(root.children[k], new_params[k])  // new_params <-- root.val, param
        return the answer if needed                              // answer <-- all ans[k]
      ```
    * Bottom-Up Approach
      * In each recursive call, we will firstly call the function recursively for all the children nodes and 
        * then come up with the answer according to the returned values and the value of the current node itself.
      * Algorithm
        ```java 
        return specific value for null node 
        for each child node root.children[k]:
          ans[k] = bottom_up(root.children[k])    // call function recursively for all children
        return answer                             // answer <- root.val, all ans[k]
        ```
  * Optimization
    * Memoization
      * By caching and reusing the intermediate results, memoization can greatly reduce the number of recursion calls, i.e. reducing the number of branches in the execution tree.
    * Tail recursion
      * Tail recursion is a recursion where the recursive call is the final instruction in the recursion function.
      * And there should be only one recursive call in the function.
      * In short, no computations are performed after the recursive call.
      * Advantage: exempted for space overhead
  * Disadvantages of recursion
    * when depth of recursion is too high, you will suffer from stack overflow
* How to identify
  * Alternate to iterative
* Example

### Heap sort
* Description
  * Heap Sort sorts a group of unordered elements using the Heap data structure.
  * Sorting algorithm using a Min Heap is as follows:
    * Heapify all elements into a Min Heap. 
    * Record and delete the top element. 
    * Put the top element into an array T that stores all sorted elements. Now, the Heap will remain a Min Heap. 
    * Repeat steps 2 and 3 until the Heap is empty. The array T will contain all elements sorted in ascending order.
  * sorting algorithm using a Max Heap is as follows:
    * Heapify all elements into a Max Heap. 
    * Record and delete the top element. 
    * Put the top element into an array T that stores all sorted elements. Now, the Heap will remain a Max Heap. 
    * Repeat steps 2 and 3 until the Heap is empty. The array T will contain all elements sorted in descending order.
* How to identify?
  * Sort an array using heap
* Time complexity: O(NlogN)
* Space complexity: O(N)

### Top K problem using Heap
* Description
  * Heap data structure to obtain Top K’s largest or smallest elements.
  * Solution 1 (Top K largest elements): 
    * Construct a Max Heap. 
    * Add all elements into the Max Heap. 
    * Traversing and deleting the top element (using pop() or poll() for instance), 
    * store the value into the result array T. 
    * Repeat last two steps until we have removed the K largest elements.
    * Similar approach can be used to find the top K smallest element
    * Time complexity: O(KlogN+N) where O(N) is used to construct heap and O(KlogN) is to remove the top elements.
    * Space complexity: O(N)
  * Solution 2 (Top K largest elements)
    * Construct a Min Heap with size K. 
    * Add elements to the Min Heap one by one. 
    * When there are K elements in the “Min Heap”, compare the current element with the top element of the Heap:
    * If the current element is no larger than the top element of the Heap, drop it and - proceed to the next element. 
    * If the current element is larger than the Heap’s top element, delete the Heap’s top element, and add the current element to the Min Heap. 
    * Repeat Steps 2 and 3 until all elements have been iterated.
    * Similar approach can be used to find the top K smallest element
    * Time complexity: O(NlogK)
    * Space complexity: O(K)
* How to identify
  * Useful in situations like Priority Queue, Scheduling
  * Find the **smallest/largest/median/top/frequent** ‘K’ elements of a given set 
* Example
  * Top ‘K’ Numbers (easy)
  * Top ‘K’ Frequent Numbers (medium) 
  * Merge K Sorted Lists (medium)
  * K Pairs with Largest Sums (Hard)

### Kth largest/smallest element using Heap
* Description
  * Use the Heap data structure to obtain the K-th largest or smallest element.
  * Solution 1 (k-th largest element)
    * Construct a Max Heap. 
    * Add all elements into the Max Heap. 
    * Traversing and deleting the top element (using pop() or poll() for instance). 
    * Repeat Step 3 K times until we find the K-th largest element.
    * Similar approach to find the kth smallest element.
    * Time complexity: O(KlogN+N)
    * Space complexity: O(N)
  * Solution 2 (k-th largest element)
    * Construct a Min Heap with size K. 
    * Add elements to the Min Heap one by one. 
    * When there are K elements in the “Min Heap”, compare the current element with the top element of the Heap:
      * If the current element is not larger than the top element of the Heap, drop it and proceed to the next element. 
      * If the current element is larger than the Heap’s top element, delete the Heap’s top element, and add the current element to the “Min Heap”. 
    * Repeat Steps 2 and 3 until all elements have been iterated.
    * Similar approach to find the kth smallest element.
    * Time complexity: O(NlogK)
    * Space complexity: O(K)
* How to identify?
  * Sometimes, useful in problems featuring a binary tree data structure
  * Sort an array to find the kth element
* Example
  * Find the Median of a Number Stream (medium)

### Breath first solution (BFS)
* Description
  * First, root node. Then, neighbours of root node. Then, neighbours of neighbours of root node and so on.
  * Use **Queue** to solve the problem
  * Need to keep track of the visited hash set
    * When there is a cycle in the traversal
    * You do not want to add the queue multiple times
* How to identify problems?
  * **Shortest or nearest or minimum distance or least distance** path from root to target node
  * Problems where you need to find the **combinations or permutations** of a given set
  * Problems featuring **Subsets pattern**
* Examples
  * Subsets With Duplicates (easy)
  * String Permutations by changing case (medium)
* Complexity
  * Traversing all the vertices
    * Time complexity: O(V+E)
    * Space complexity: O(V)
  * Shortest path 
    * Time complexity: O(V+E)
    * Space complexity: O(V)
  * Traversing all paths
    * Time Complexity: O(2^V * V)
    * Space Complexity: O(2^V * V)
      * https://leetcode.com/explore/learn/card/graph/620/breadth-first-search-in-graph/3854/

### Depth first solution (DFS) 
* Use cases
  * **deep copy or visit all nodes or fill nodes with a new value** of a graph
  * Traverse all vertices in a “graph”;
  * Traverse all paths between any two vertices in a “graph”.
  * Used to construct a linked list
  * Use **Stack or recursive**  to solve the problem
  * Need to keep track of visiting nodes (Nodes in the current traversal)
    * When there is a cycle in the traversal 
    * You do not want to traverse the same node multiple times
  * Need to keep track of visited nodes (Nodes which are already visited)
    * When the graph is not connected
* Complexity
  * V is the number of vertex and E is the number of edges.
  * Traversing all the vertices
    * Time complexity: O(V+E)
    * Space complexity: O(h) where h is the maximum depth of the graph
  * Traversing all the paths
    * Time complexity: O((V-1)!) or O(2^V * V)
    * Space complexity: O(V^3) or O(V)
    * Explanation: https://leetcode.com/explore/learn/card/graph/619/depth-first-search-in-graph/3848/
      * https://leetcode.com/explore/learn/card/graph/619/depth-first-search-in-graph/3850/

### Backtracking
* Description
  * DFS handles an explicit graph.While Backtracking handles an implicit graph.
  * Depth First Search is a special type of backtracking algorithm.
  * Backtracking can stop (finish) searching certain branch by checking the given conditions (if the condition is not met)
    * in DFS, you have to reach to the leaf node of the branch to figure out if the condition is met or not, 
      * so you cannot stop searching certain branch until you reach to its leaf nodes.
  * If you have backtracking, you have recursion.

### Topological sort
* Description
  * Sort the vertices in a graph based on the dependencies
  * Build the adjacency graph 
  * Identify nodes with zero dependencies
  * Based on the identified nodes, find all the adjacent nodes and remove this node dependency
    * When the adjacent node dependencies is zero
    * add to the list of identified nodes
* How to identify ?
  * The problem will deal with graphs that have no directed cycles
  * If you’re asked to update all objects in a sorted order
  * If you have a class of objects that follow a particular order
* Examples
  * Task/Course scheduling (medium)
  * Minimum height of a tree (hard)

### Dynamic programming
* Description
* How to identify ?
  * Count of the total iterations for a specific problem e.g.
* Examples

### Knapsack

### Bit Manipulation
* Description
  * Bitwise XOR
* How to identify ?
* Examples

### Local min and max
### Matrix rotation

## Sorting

### Quick sort

### Merge sort

### Radix sort

### Tim sort

### Disjoint Set - Quick find
* Description
  * Use array as a auxillary datastructure
    * Array index will denote the vertex value
    * Array value will be the root of the vertex
  * Find
    * Store the root vertex as the value for particular index in the array
  * Union
    * find the root of vertex X and Y
    * For every element in the array, when they don't match
      * replace the array element rootY with rootX i.e. vertex new root would be rootX after union.
* How to identify?
  * Find whether two vertex are connected in a graph or not
* Time complexity
  * find function - O(1)
  * union function - O(N)
  * Initialization - O(N)
* Space complexity: O(N)

### Disjoint Set - Quick union
* Description
  * Use array as a auxillary datastructure
    * Array index will denote the vertex value
    * Array value will be the parent/root of the vertex
  * Find
    * Traverse the parent until the root of the vertex is found.
  * Union
    * find the root of vertex X and Y
    * When they don't match, replace the rootY with rootX i.e. vertex Y's new root would be rootX
* How to identify?
  * Find whether two vertex are connected in a graph or not
* Time complexity
  * find function - O(log N). In worst case, it is O(N).
  * union function - O(log N). In worst case, it is O(N).
* Space complexity: O(N)

### Disjoint Set - Union by Rank
* Description
  * Optimization to avoid skewed trees.
  * Choosing the parent node based on certain criteria (by rank), we can limit the maximum height of each vertex.
  * “rank” refers to the height of each vertex.
  * Find function
    * Traverse the parent until the root of the vertex is found.
  * Union function
    * choose the root node of the vertex with a larger “rank”.
    * Merge the shorter tree under the taller tree and assign the root node of the taller tree as the root node for both vertices.
* How to identify?
  * Find whether two vertex are connected in a graph or not
* Time complexity
  * find function: O(log N)
  * union function: O(log N)
* Space complexity
  * O(N)

### Disjoint Set - Path compression Optimization
* Description
  * optimization to avoid re-computation of find function
  * finding the root node, we can update the parent node of all traversed elements to their root node.
  * Will use recursion to update the parent nodes
  * Find function
    * Use recursion to update the parent node of all traversed elements
  * Union function
    * find the root of vertex X and Y
    * When they don't match, replace the rootY with rootX i.e. vertex Y's new root would be rootX
* How to identify?
  * Find whether two vertex are connected in a graph or not
* Time complexity
  * find function: O(log N) - Average case
  * union function: O(log N) - Average case
* Space complexity


