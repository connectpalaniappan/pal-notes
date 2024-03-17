Sharding for high availability and consistency

* Estimate database growth, maintainance and reliability and future.


### Partitioning methods

#### Horizontal partitioning or sharding

#### Vertical partitioning

#### Directory based partitioning


### Partitioning Criteria

#### Key or hash based partitioning

#### Consistent Hashing
* Basic Consistent Hashing 
  * hash the key and partition based on the range
* Virtual Nodes
  * hash the key
  * instead of a server mapped to a single range, it can be mapped to multiple smaller ranges to spread distribute load evenly.  

#### List partitioning

#### Round-robin partitioning

#### Composite partitioning


### Partitioning problems

#### Joins and denormalization

#### Referential integrity

#### Rebalancing


### Partitioning agreement

#### Quorum 

#### Leader-follower 
* Avoid write to read-replicas. Ensure appropriate permission are implemented. 
  [Reddit insfrastructure](https://youtu.be/nUcO7n4hek4?t=1117)