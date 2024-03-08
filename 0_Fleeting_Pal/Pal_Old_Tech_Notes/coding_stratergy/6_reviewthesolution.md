
* Review the solution with the use cases defined in step 1.
* Always check for exceptions i.e. invalid cases
* Write down TODOs to show you know a better approach

## Common Pitfalls (Gotchas)

### Numbers
* Divide by zero error.

### Linkedlist
* Nullpointer assignment

### Doubly linkedlist
* When you do optimization such as dummyhead, dummytail and length, 
  ensure those are properly implemented in addNode, deleteNode and getNode functions.
* 

### Hashmap
* Check whether there can be **duplicate keys**. If yes, would you throw an exception or store the values in a list.
* When you need to remove elements from the map, don't do it when you are traversing, 
  you will end up in **ConcurrentModificationException**. Remove each element, validate and if necessary, 
  add it back to the element.

### Depth first search
* Remember to check for visited nodes
