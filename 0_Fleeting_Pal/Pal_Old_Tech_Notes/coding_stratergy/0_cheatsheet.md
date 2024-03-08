
## Steps to solve any question
1. [Repeat the question to understand the outcome]()
   1. [Multiple questions]() - Solve one question at a time
2. [Break down the problem into a set of preconditions](#preconditions-to-identify-the-solution)
   1. Identify pre-conditions based on key-terms
3. [Write good use/edge cases](#use-casesedge-cases)
   1. Identify pre-conditions based on use cases
4. [Discuss brute force solution](#preconditions-to-identify-the-solution) 
5. [Discuss optimized solution]()
   1. Break down and optimize components in your brute force solution
   2. [Optimize time complexity](#time-complexity-optimization-pattern)
   3. [Optimize space complexity](#space-complexity-optimization-pattern)
   4. Keep iterating until satisfied
6. [Discuss time and space complexities for optimized solution]()
8. [Implement the optimized solution]()
9. [Test the solution with your test cases]()
10. [Solve the bugs]()
11. [Ask for suggestions]()

### Preconditions to identify the solution
Think of an algorithm/data structure as a way of getting a desired outcome based on a series of preconditions. 
Once you meet these preconditions, you can apply the algorithm to get the desired outcome.
Here, Outcome is the main point and preconditions are the sub-point.
1. [Algorithm pattern]()
    1. Processing order
       1. [random iteration]() - nested loops
       2. [in-place operation]() - two pointer array/linked list
       3. [process in-order]() - queue processing
       4. [infer past/future data]() - stack processing
    2. Stack traversal
       1. [min/max in stack]() - extra stack to track min/max
    3. LinkedList traversal
       1. [determine cycles in linked list]() - fast and slow pointer
    4. Search for an element
       1. [any data structure]() - linear traversal
       2. [Sorted array]() - Binary search algorithm; min/max/at least/at most/largest min/smallest max
       3. [values match the index position]() - cyclic sort
       4. [pattern match in substring]() - sliding window
    5. Search based on a key
       1. [Group and search for duplicates]() - hash algorithm
       2. [Group and search based on key]() - hash algorithm 
       3. [Cache: search for previous computed result]() - hash algorithm used with optimizing dynamic programming
    6. Min/Max
       1. [Top K items]() - Heap sort (priority queue)
       2. [kth largest/smallest element]() - heap sort (priority queue)
    7. Merge interval
       1. [Merge overlapping intervals]() - merge interval algorithm (stack)
       2. [Scheduling]() - priority queue
    8. Traverse tree
       1. [Binary search tree]() - in-order (stack)
       2. [Top down approach]() - pre-order (stack)
       3. [Bottom down approach]() - post order (stack)
       4. [level traversal]() - breath first search (queue)
    9. Search for shortest path
        1. [Equal positive weights in graph]() - breath first search (queue)
        2. [Equal positive weights - Find all paths and then the shortest]() - depth first search (stack)
        3. [Unequal Positive weights in graph]() - Dijkstra
        4. [Unequal Negative weights in graph]() - Bellman ford algorithm
    10. Search all vertex/path
        1. [One path to reach specific destination]() - Depth first search (stack)
        2. [Exhaustive search - all permutation/combination - multiple paths]() - recursive backtracking
        3. [] - iterative breadth first search
    11. Sort dependency graph
         1. [Graph vertices in dependency order]() - topological sort
         2. [Traversing all the vertices]() - Depth first search 
    12. Connect graph vertex
         1. [based on the connected edges]() - Disjoint quick union or union find
         2. [with minimum cost]() - Minimum spanning tree (Kruskal algorithm, Prim Algorithm)
    13. [Optimize for the best]() - Greedy
    14. []() - subsets
    15. [Divide into smaller subproblems]()
        1. [Focus on the base case]() - Recursive solution
        2. [Remember previous computation]() - Dynamic programming; maximum/minimum subarray/subset/options
3. [Datastructures pattern]()
    1. Efficient storage of all values
       1. [Insertion order]() - LinkedList
          1. *Advantage: Modification easier*
    2. [Word search]()
       1. [Faster key lookup]() - Hashmap
          1. *Advantage: Better time complexity O(1)*
          2. *Disadvantage: Worst in space complexity*
       2. [find some common substring among a set of strings]() - Trie
          1. *Advantage: Efficient in space complexity*
          2. *Disadvantage: Worst time complexity O(n)*
    4. Process in order
       1. [first added element first]() - queue
       2. [last added element first]() - stack
    5. Search
       1. [Based on index]() - Arrays
       2. [Based on keys, No duplicates]() - HashSet/HashMap
    6. Sort
       1. [Sort - Min/Max - Duplicates allowed]() - Priority Queue
    7. Search and sort
       1. [Search based on keys, No duplicates]() - TreeSet/TreeMap
       2. [Previous/Next element - first vs last being the min vs max]() - Binary search tree
    8. [Connected points]() - Disjoint set
    9. [Source to destination]() - Graph

### Time Complexity optimization pattern
* O(N^N): 
* O(N!): Travelling salesman problem via brute-force 
* O(2^N, 3^N): Permutation (usually NP hard problems), factorial via brute-force
* O(N^2, N^3): Recursion/generate subsets, nested loops
* O(N logN): sorting/heap, binary search tree
* O(N): Iteration, pointers/sliding window, common array operations
* O(log N): binary search/exponentially sized steps search
* O(1): hashmap or index of array

### Space Complexity optimization pattern
* O(V+E): Graph vertex plus edge
* O(N): Array, hashmap, priority queue,
* O(1): Single variable

### Use cases/Edge cases
Good test cases have good code coverage.
Each of these tests should be independent of one another
1. [Algorithm specific cases]()
    1. [Two pointer]()
    2. [Binary search]()
        1. [Data structure sorted or not]()
    3. [Sliding window]()
    4. [Merging interval]()
        1. [overlap interval i.e. A.end > B.start]()
        2. [overlap interval i.e. A.end < B.start]()
        3. [overlap at edge i.e. A.start = B.start]()
        4. [no overlap]()
    5. [Greedy]()
    6. [Breadth first search]()
       1. Pre-requisite questions
          1. [when elements to process during level-order traversal]()
             1. **Process elements at the current level**
             2. **Process elements at the next level**
                1. *Advantage: No need queue when the graph is a perfect binary tree*
       2. Implementation questions
          1. [How to perform level-order traversal]()
             1. **Track the node along with level number**
                1. *Disadvantage: Need extra data structure**
             2. **Have a demarcation node such as NULL to determine the end and start of an level**
                1. *Disadvantage: Extra demarcation node storage and complexity**
             3. **Have a for-loop based on the queue-size**
    7. [Depth first search]()
       1. [Reached all the leaf nodes/paths]()
    8. [Backtracking]() - Exhaustive search - all permutation/combination - multiple paths
       1. [Condition is not satisfied in the traversal]() - break and return to the parent
       2. [Condition is satisfied in the traversal]()
       3. [Reached the leaf node]()
    9. [Topological sort]()
    10. [Minimum spanning tree]()
         1. [Minimum condition to join vertexes]()
         2. [Virtual nodes to represent vertex weight]()
    11. [Disjoint set - Quick find/Quick union]()
    12. [Dynamic programming]()
2. [Datastructures Specific cases]()
    1. [Numbers]()
       1. [positive or negative or zero]()
       2. [float or double or only int]()
       3. [even or odd number]()
       4. [Maximum or Minimum value]()
       5. [Overflow capacity]()
           1. *int - max capacity - 2^32 ~ 2.1e9 ~ 10^9*
           2. *long - max capacity - 2^63 ~ 9.2e18 ~ 10^18*
    2. [String]()
       1. [null or empty]()
       2. [alphanumeric]() - uppercase? lowercase? numbers?
       3. [special characters]() - spaces? punctuation?
       4. [Different languages]() - Diacritics? unicode compliant? ASCII? Emoji?
    3. [Single dimensional array]()
       1. [Null or empty]()
       2. [Elements range]()
       3. [Duplicate elements]()
       4. [sorted or reversed sorted]()
       6. [Nested or not nested]()
    4. [Two dimensional array]()
       1. [Null or empty]()
       2. [one element]()
       3. [valid element next or not next to boundary]()
       4. [traversal]() - left? right? up? down?
    5. [Circular array]()
    6. [Tuples]()
       1. [Named elements]()
    7. [Single linked List]()
       1. [null or empty]()
       2. [Elements range]()
       3. [Duplicate elements]()
       4. [sorted or reversed sorted]()
       5. [Cyclic]()
       6. [Circular]()
    8. [Double linked list]()
    9. [HashSet]()
       1. [null]()
       2. [key not present]()
          1. **null**
          2. **default value**
       3. [keys range]() - to define hashcode to avoid collisions
       4. [if collisions happens]()
          1. **throw an exception**
          2. **store the values in a list**
    10. [Hashmap]()
        1. hashset testcases
        2. [key are added repeatedly]()
           1. **skip**
           2. **override value**
    11. [Queue]()
        1. [null]()
        2. [poll on empty queue (size ==0)]()
        3. [offer on full queue (size == capacity)]()
        4. [poll/offer on stack (size == capacity)]()
    12. [Stack]()
        1. [null]()
        2. [pop on empty stack]()
        3. [push on full stack (size == capacity)]()
           1. *Throw error*
           2. *Drop the last element and push the latest one*
        4. [push/pop on stack (size < capacity)]()
    13. [Tree]()
        1. [root is null]()
        2. [only root is present]()
        3. [root with only left child]()
        4. [root with only right child]()
        5. [root with both left and right child]()
    14. [Binary tree]()
        1. Tree test cases
        2. [Complete or skewed binary tree]()
    15. [Binary search tree]()
        1. Tree test cases
        2. Binary tree test cases
        3. [sorted or reversed sorted]()
    16. [Graph]()
        1. Pre-requisite questions
           1. [Is the graph directional or not]() - Directed vs undirected
              1. **directed graph**
                 1. *Add one edge based on direction in graph representation*
              2. **undirected graph**
                 1. *Add edge for both vertex in graph representation*
                 2. *Visited data structure to track for already visited nodes*
           3. [Is the graph cyclic or not]() - Cyclic vs Acyclic
               1. **Acyclic**
               2. **Cyclic**
                  1. *Visited data structure to track already visited vertex*
           4. [Is the graph connected or not]()
              1. **Connected**
              2. **Disconnected**
                 1. *Start traversal from unvisited node*
           5. [Vertexes with duplicate values]()
               1. **Visited check should be based on node reference not node value**
           6. [Vertexes with self edges]()
              1. **Visited data structure to track already visited vertex**
           7. [Edges with same source and destination vertex]()
               1. **Ignore the duplicate**
               2. **Add a counter in adjacency list to track the duplicate**
        2. Implementation decisions
           1. [How to represent graph]()
               1. **Adjacency list** - vertex is string/character
               2. **Adjacency matrix** - vertex is integer
                  1. *Visited can be tracked in the matrix*
           2. [How to represent visited]()
              1. **Empty set**
              2. **Array values filled with boolean false**
           3. [When to create the adjacency list]()
               1. **Pre-create: Before solving the problem**
                  1. *Advantage: Provides more clarity as you divide the problem*
               2. **Inline: Create as you solve the problem**
           4. [How to verify all edges are covered]()
              1. **Remove the edges from primary adjacency list as you traverse the graph**
              2. **Create a secondary adjacency list to check with primary adjacency list whether an edge has been traversed or not**
           5. []
    17. [Disjoint set]()
        1. [Condition for the root]()
3. [Output Datastructures]()
   1. [Modify input]()
   2. [New datastructures]()
4. [Implementation]()
   1. [How many function calls made]()
   2. [Usage]()
       1. [Built in functions ok]() - String.reverse
       2. [Higher order functions]() - map, filter, and reduce
   3. [Approach]()
       1. [Recursive or iterative]()
