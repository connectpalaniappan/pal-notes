## CAP theorem

### Consistency
* Every read receives the most recent write or an error
* Information needs to be accurate

### Availability
* Every request receives a (non-error) response, without the guarantee that it contains the most recent.
* Information needs to be available not accurate.

### Partition Tolerance
* The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes.
* Network issues are inevitable

