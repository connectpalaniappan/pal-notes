
## Implementation tricks and techniques

### Merge overlapping intervals
```java
int start = interval[0], end = interval[1];
// if there is no overlap, just add an interval
if (output.getLast()[1] < start) {
    output.add(interval);
    // if there is an overlap, merge with the last interval
}
else {
    interval = output.removeLast();
    interval[1] = Math.max(interval[1], end);
    output.add(interval);
}
```

### Depth first search
* When the input is an array, use it as the output array and also use it as a way to check whether a cell has been visited or not. 

