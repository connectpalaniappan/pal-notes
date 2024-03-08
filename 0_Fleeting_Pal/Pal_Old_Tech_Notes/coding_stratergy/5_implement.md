
* Write down your approach and agree with the interviewer.
    * You can't think and implement at the same time. Split this.
* Solve the problem.
  * Start with a brute-force solution
  * Use data structures to identify optimal solution
  * Mention the space/time complexity
* Listen and follow any tricks your interviewer provides in the process.
    * Discuss alternatives but follow interviewer approach

## Implementation tricks and techniques

## In-built functionalities
| Use case | Java (Java methods)|
| :---        |    :----:   | 
| Binary string to Integer | Integer.parseInt(binaryString, 2) | 
| List to array | output.toArray(new int[output.size()][2]) |

### Sorting with custom comparator
* Arrays.sort() is implemented as a variant of quicksort algorithm 
  * Time complexity is O(NlogN) 
  * space complexity is O(logN)
```java
Arrays.sort(intervals, (a,b) -> Integer.compare(a[0], b[0]));
```

### Arrays - copy
* Arrays copy the first k elements
```java
Arrays.copy(array, k);
```

### Arrays - fill
* Fill a boolean array with all values as false.
```java
Arrays.fill(seen, false);
```


### Pass by reference vs pass by value
Be careful with pass by reference vs pass by value
* pass by value
  * all primitives, Integer, String, Arrays
* pass by reference
  * StringBuilder
