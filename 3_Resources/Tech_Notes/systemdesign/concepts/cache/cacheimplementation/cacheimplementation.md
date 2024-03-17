## Algorithm
* Adaptive Replacement Cache (ARC)
* Least recently used
TODO

#### Requirements
- Functional
    - put(key, value)
    - get(key)
- Non-functional
    - Scalable
    - Highly available
    - Highly performant

#### Single node solution
- Hashmap with key,value pair
- Eviction or replacement policy
    - Least recently used policy
        - Doubly linked list to identify the least frequently used item

#### Distributed solution
- On a separate node vs as a separate process on the same service node
- Identify which shard
    - CacheHostNumber = HASH_FUNCTION(Key) MOD Numberofcachehosts
        - Poor when there are hardware failures. Riskier when the failed hardware comes back.
    - Consistent hashing
- cache client
    - Use cache client to determine which shard. Cache client is a part of the service.
    - Cache client knows about all the cache servers
    - all cache clients should have the same list of servers
    - client stores the list of servers in sorted map e.g. by hash value i.e. treemap in java
    - binary search is used to identify the server O(log(n))
    - Cache client uses TCP or UDP protocol to talk to servers
    - if server is unavailable, client proceeds as though it was a cache miss.
- Maintaining the list of cache servers
    - Configuration management tools such as chef or puppet
    - On a storage such as S3 and pulls configs periodically.
    - Configuration service such as zookeeper
- High availability achieved using master-slave architecture.
    - Updates to follower are made synchronously.
    - Master selection can be made by a configuration service.
- Hot shard problem
    - Master-slave replication
- Synchronous replication of cache servers lists to avoid conflicts
    - Would increase latency and system complexity.
- Key expiration
    - passively expire an item when someone tries to access it and the item is found to be expired
    - actively expire, maintainance thread to clean expired items.
- local and distributed cache can be used simultaneously.
- security
    - cache server behind firewall and only approved servers have access to it.
    - Encrypt and decrypt data before storing and on its way out
- Monitoring and logging
    - Metrics
        - number of faults while calling cache
        - latency
        - number of hits and misses
        - CPU and memory utilization on cache hosts
        - Network I/O

### Reference
https://youtu.be/iuqZvajTOyA
[https://drive.google.com/file/d/1mCzLum_E3WMjrAzN2j2FdK0o6d_11mcm/view?usp=sharing](https://drive.google.com/file/d/1mCzLum_E3WMjrAzN2j2FdK0o6d_11mcm/view?usp=sharing)