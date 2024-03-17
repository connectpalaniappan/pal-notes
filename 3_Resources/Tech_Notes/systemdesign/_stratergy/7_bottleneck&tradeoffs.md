
Tradeoffs
1. [Impact in changing a component](#impact-in-changing-a-system)
2. [Data: Is the content already encoded](#data-is-the-content-already-encoded)
3. [Client: Peer-to-peer communication security concern](#client-peer-to-peer-communication-security-concern)
4. [Client: Peer-to-peer communication consistency concerns](#client-peer-to-peer-communication-consistency-concerns)
5. [Client: Saving metadata locally only](#client-saving-metadata-locally)
6. [Client: Space restriction on desktop client](#client-space-restriction-on-desktop-client)
7. [Client: Conflicts in concurrent or offline editing](#client-conflicts-in-concurrent-or-offline-editing)
8. [Client: Chunk a file or not](#client-chunk-a-file-or-not-on-client)
9. [Client: Chunk size - large or small](#client-chunk-size-large-or-small)
10. [Client: Dropped chunk in files](#client-dropped-chunk-in-files)
11. [Client: Individual vs Buffering/Batching requests](#client-individual-vs-bufferingbatching-requests)
12. [Client: Response content in bulk vs pagination](#client-response-content-in-bulk-vs-pagination)
13. [Client: Saving metadata or not](#client-saving-metadata-or-not)
14. [Client: Sync updates immediately or on-demand or both](#client-sync-updates-immediately-or-on-demand-or-both)
15. [Client: Different routes for data and control flow](#client-different-routes-for-data-and-control-flow)
16. [Client: Push vs pull vs hybrid](#client-push-vs-pull-vs-both)
17. [Client: Send entire data or differential updates](#client-send-entire-data-or-differential-updates)
18. [Client: Broadcast to multiple or send to one client](#client-broadcast-to-multiple-or-send-to-one-client)
19. [Client: How to send data to offline clients](#client-how-to-send-data-to-offline-clients)
20. [Client: How to send data to offline users](#client-how-to-send-data-to-offline-users)
21. [Long polling vs polling](#long-polling-vs-polling)
22. [Long polling vs Server send event](#long-polling-vs-server-send-event)
23. [Server send events vs websocket connection](#server-send-events-vs-websocket-connection)
24. [Websocket: permanent via health check vs re-establish connection](#websocket-permanent-via-health-check-vs-re-establish-connection)
25. [DNS: Single vs multiple domain](#dns-single-vs-multiple-domain)
26. [DNS: How to determine routing strategy](#dns-how-to-determine-routing-strategy)
27. [Load balancer: How to determine which service is up or down](#load-balancer-how-to-determine-which-service-is-up-or-down)
28. [Load balancers vs API Gateway](#load-balancers-vs-api-gateway)
29. [Load balancers vs reverse proxy](#load-balancers-vs-reverse-proxy)
30. [Load balancers: Software vs Hardware](#load-balancers-software-vs-hardware)
31. [Load balancer: Layer 4 vs Layer 7](#load-balancer-layer-4-vs-layer-7)
32. [Load balancer algorithm](#load-balancer-algorithm)
33. [Load balancers: Single vs multiple](#load-balancers-single-vs-multiple)
34. [Load balancer vs Reverse proxy](#load-balancers-vs-reverse-proxy)
35. [Service: Monolith vs microservice](#service-monolith-vs-microservice)
36. [Service: Handle race conditions](#service-handle-race-conditions)
37. [Service: In-memory computation or storage](#service-in-memory-computation-or-storage)
38. [Service: Process requests/events in order or un-ordered manner](#process-requestsevents-in-order-or-un-ordered-manner)
39. [Service: Historical data might impact performance](#service-historical-data-might-impact-performance)
40. [Service: Push vs pull vs in-process](#service-push-vs-pull-vs-in-process)
41. [Service: Computation on the fly errors](#service-computation-on-the-fly-errors)
42. [Ensure idempotency: Same data is returned always](#ensure-idempotency-same-data-is-returned-always)
43. [Service: APIGateway vs custom service](#service-apigateway-vs-custom-service)
44. [In-house vs open source vs managed](#in-house-vs-open-source-vs-managed)
45. [Service: Ambassador service vs service proxy for cross-cutting concerns]()
46. [Service: Pre-compute or compute-on-the-fly](#service-pre-compute-or-compute-on-the-fly)
47. [Service: Routing - based on what should we split data](#service-routing---based-on-what-should-we-split-data)
48. [Server: Single vs multi-threaded processing](#server-single-vs-multi-threaded-processing)
49. [Server: Multi-threaded- serial vs parallelism vs concurrency](#server-multi-threaded--serial-vs-parallelism-vs-concurrency)
50. [Server: Multi-threaded - Blocking vs Non-blocking IO](#server-multi-threaded---blocking-vs-non-blocking-io)
51. [Database: Consistency vs Availability](#database-consistency-vs-availability)
52. [Database: ACID vs BASE](#database-acid-vs-base)
53. [Database: SQL vs NoSQL](#database-sql-vs-nosql)
54. [Database: Row vs column oriented](#database-row-vs-column-oriented)
55. [Database: Handle inconsistency issue with multiple masters](#database-handle-inconsistency-issue-with-multiple-masters)
56. [Object storage: hot or cold](#object-storage-hot-or-cold)
57. [Object storage: Do you need to encrypt file or not](#object-storage-do-you-need-to-encrypt-file-or-not)
58. [Cache/Database: Optimized for querying vs writing](#cachedatabase-optimized-for-querying-vs-writing)
59. [Cache stampede or thundering herd or cache miss attack](#cache-stampede-or-thundering-herd-or-cache-miss-attack)
60. [Cache overhead in updating the stale content](#cache-overhead-in-updating-the-stale-content)
61. [Cache placement](#cache-placement)
62. [Cache updates](#cache-updates)
63. [Cache eviction policies](#cache-eviction-policies)
64. [Cache memory vs latency](#cache-memory-vs-latency)
65. [CDN content authorization checks](#cdn-content-authorization-checks)
66. [CDN: Overhead in updating the content](#cdn-overhead-in-updating-the-content)
67. [CDN vs microservice reads](#cdn-vs-microservice-reads)
68. [CDN: push vs pull](#cdn-push-vs-pull)
69. [CDN: Local vs global](#cdn-local-vs-global)
70. [Consistency: Strong vs eventual](#consistency-strong-vs-eventual)
71. [Consistency: Single vs distributed transaction](#consistency-single-vs-distributed-transaction)
72. [Single transaction: Pessimistic vs Optimistic concurrency control](#single-transaction-pessimistic-vs-optimistic-concurrency-control)
73. [Single transaction: isolation levels](#single-transaction-isolation-levels)
74. [Distributed transaction: Conflict ignored vs avoidance vs detection](#distributed-transaction-conflict-ignored-vs-avoidance-vs-detection)
75. [Sharding: Data suitability](#sharding-data-suitability)
76. [Sharding: How to avoid hot shards](#sharding-how-to-avoid-hot-shards)
77. [Shard outage affect a set of users](#shard-outage-affecting-a-set-of-users)
78. [Sharding: routing at application layer vs external proxy](#sharding-routing-at-application-layer-vs-external-proxy)
79. [Sharding: partitioning strategy - based on what should we split the data](#sharding-partitioning-strategy---based-on-what-should-we-split-the-data)
80. [Sharding: Once sharded how do you find the shard](#sharding-once-sharded-how-do-you-find-the-shard)
81. [Sharding: Logical vs physical](#sharding-logical-vs-physical)
82. [Sharding vs read-replicas](#sharding-vs-read-replicas)
83. [Horizontal vs vertical partitioning](#database-horizontal-vs-vertical-partitioning)
84. [Consistency: Handle partial failures](#consistency-handle-partial-failures)
85. [Availability: Single point of failure](#availability-single-point-of-failure)
86. [Replication vs Consensus](#replication-vs-consensus)
87. [Availability: Replication encoding scheme](#availability-replication-encoding-scheme)
88. [Replicas: Synchronous vs Asynchronous replication in SQL databases](#replicas-synchronous-vs-asynchronous-replication-in-sql-databases)
89. [Replicas: Synchronous - writes to master or all replicas](#replicas-synchronous---writes-to-master-or-all-replicas)
90. [Leader selection algorithm](#leader-selection-algorithm)
91. [Leaderless replication: choice for coordinator node](#leaderless-replication-choice-for-coordinator-node)
92. [Leaderless replication: Number of quorum reads vs writes](#leaderless-replication-number-of-quorum-reads-vs-writes)
93. [Consensus algorithm](#consensus-algorithm)
94. [Service discovery: Client vs server side](#service-discovery-client-vs-server-side)
95. [Service discovery: where to place](#service-discovery-where-to-place)
96. [Resiliency: Load shedding vs managing load](#resiliency-load-shedding-vs-managing-load)
97. [Resiliency: Automatic vs manual](#resiliency-automatic-vs-manual)
98. [Resiliency client: drop or retry failed requests](#resiliency-client-drop-or-retry-failed-requests)
99. [Resiliency client: Retry requests - Exponential backoff vs jitter to avoid retry storm](#resiliency-client-retry-requests---exponential-backoff-vs-jitter-to-avoid-retry-storm)
100. [Resiliency client: Timeout vs circuit breaker](#resiliency-client-timeout-vs-circuit-breaker)
101. [Resiliency client: Timeout - Connection and request timout values](#resiliency-client-timeout---connection-and-request-timout-values)
102. [Resiliency client: Circuit breaker - Error threshold vs timeouts](#resiliency-client-circuit-breaker---error-threshold-vs-timeouts)
103. [Priority queue topology](#priority-queue-topology)
104. [Priority queue: preempt or continue processing a low priority message when a high priority message arrives](#priority-queue-preempt-or-continue-processing-a-low-priority-message-when-a-high-priority-message-arrives)
105. [Priority queue: Upgrade message priority dynamically or not](#upgrade-message-priority-dynamically-or-not)
106. [Messaging: Queue messages that end up in failure](#messaging-queue-messages-that-end-up-in-failure)
107. [Messaging: Queue messages that can't be processed](#messaging-queue-messages-that-cant-be-processed)
108. [Messaging: Queue messages expiry time](#messaging-queue-messages-expiry-time)
109. [Messaging: Queue messages to be grouped](#messaging-queue-messages-to-be-grouped)
110. [Messaging: Queue messages to be scheduled](#messaging-queue-messages-to-be-scheduled)
111. [Messaging: When the entire queue cluster is not available](#messaging-when-the-entire-queue-cluster-is-not-available)
112. [Messaging: Partition the queue or not](#messaging-partition-the-queue-or-not)
113. [Messaging: Publisher need or need not decide on partitioning strategy](#messaging-publisher-need-or-need-not-decide-on-partitioning-strategy)
114. [Messaging: Subscription pattern](#messaging-subscription-pattern)
115. [Messaging: Checkpointing - Commit individual or group of messages](#messaging-checkpointing---commit-individual-or-group-of-messages)
116. [Messaging: Consumer: Single vs multiple consumer for queues](#consumer-single-vs-multiple-consumer-for-queues)
117. [Messaging: Single vs multi-threaded consumer](#messaging-single-vs-multi-threaded-consumer)
118. [Analytics: Batch vs stream vs both](#analytics-batch-vs-stream-vs-both)
119. [Analytics: Batch processing - What is our batching strategy](#analytics-batch-processing---what-is-our-batching-strategy)
120. [Communication message format](#communication-messaging-formats)
121. [Communication architecture style](#communication-architecture-style)
122. [Communication protocol](#communication-protocols)
123. [Communication spec](#communication-spec)
124. [Communication patterns](#communication-patterns)
125. [OSI layer protocols](#osi-layer-protocols)
126. [Serialization vs encoding vs Hashcode](#serialization-vs-encoding-vs-hashcode)
127. [Interface vs schema](#interface-vs-schema)
128. [Private vs public IP Address](#private-vs-public-ip-address)
129. [Kubernetes vs Virtual machines](#kubernetes-vs-virtual-machines)

### Impact in changing a system
* You can easily identify the impacts in changing a component, 
  * by understanding the impact on its dependent components.
* Solving a graph problem. 
  * Poorly build component is going to impact its dependencies.

### Data: Is the content already encoded

### Client: Peer-to-peer communication security concern

### Client: Peer-to-peer communication consistency concerns

### Client: Saving metadata locally

### Client: Space restriction on desktop client

### Client: Conflicts in concurrent or offline editing

### Client: Chunk a file or not on client
* Better to chunk a file on the client side
* Files can be stored in small parts or chunks (say 4MB)
* all failed operations shall only be retried for smaller parts of a file. 
  * If a user fails to upload a file, then only the failing chunk will be retried.
* Reduce the amount of data exchange by transferring updated chunks only.
* Removing duplicate chunks, we can save storage space and bandwidth usage.
* For small changes, clients can intelligently upload the diffs instead of the whole chunk.

### Client: Chunk size large or small
* Chunk size based on 
  * Storage devices we use in the cloud to optimize space utilization and input/output operations per second (IOPS) 
  * Network bandwidth 
  * Average file size in the storage etc.

### Client: Dropped chunk in files

### Client: Individual vs Buffering/Batching requests
Individual request:
* 
Buffering/Batching requests on the client
* Increases throughput and increases latency
* Introduces complexity on how to handle failures in the batch
  * Resend the whole batch or only failures.

### Client: Response content in bulk vs pagination

### Client: Saving metadata or not
* Keeping a local copy of metadata not only enable us to do offline updates 
* Saves a lot of round trips to update remote metadata.

### Client: Different routes for data and control flow

### Client: How to send data to offline clients
* If the receiver has disconnected, the server can notify the sender about the delivery failure. 
* If it is a temporary disconnect, e.g., the receiver’s long-poll request just timed out, then we should expect a reconnect from the user. 
  * In that case, we can ask the sender to retry sending the message. 
* This retry could be embedded in the client’s logic so that users don’t have to retype the message. 
* The server can also store the message for a while and retry sending it once the receiver reconnects.

### Client: How to send data to offline user
* Push notification
  * User’s can only send messages to active users 
  * if the receiving user is offline, we send a failure to the sending user. 
  * Push notifications will enable our system to send messages to offline users.
  * For Push notifications, each user can opt-in from their device (or a web browser) to get notifications whenever there is a new message or event. 
  * Each manufacturer maintains a set of servers that handles pushing these notifications to the user.
  * To have push notifications in our system, we would need to set up a Notification server, which will take the messages for offline users and send them to the manufacture’s push notification server, which will then send them to the user’s device.

### Client: Send entire data or differential updates
* Better to send differential updates
  * Service can employ a differencing algorithm to reduce the amount of the data that needs to be synchronized. 
  * Instead of transmitting entire files from clients to the server or vice versa, we can just transmit the difference between two versions of a file. 
  * Therefore, only the part of the file that has been changed is transmitted. 
  * This also decreases bandwidth consumption and cloud data storage for the end user.
  * Server and clients can calculate a hash (e.g., SHA-256) to see whether to update the local copy of a content or not. 
  * On the server, if we already have a content with a similar hash (even from another user), we don’t need to create another copy, we can use the same content.

### Client: Broadcast to multiple or send to one client


### Client: Sync updates immediately or on-demand or both

### Client: Push vs pull vs both
* Pull
  * Clients can pull the contents from the server on a regular basis or manually whenever they need it. 
  * Possible problems with this approach are 
    * New data might not be shown to the users until clients issue a pull request 
    * Most of the time pull requests will result in an empty response if there is no new data.
    * Server needs to keep track of messages that are still waiting to be delivered
    * To minimize latency for the user, they have to check the server quite frequently
  * Push is real-time but lot more expensive
* Push
  * Servers can push new data to the users as soon as it is available. 
  * To efficiently manage this, users have to maintain a Long Poll request with the server for receiving the updates. 
  * A possible problem with this approach is, a user who follows a lot of people or a celebrity user who has millions of followers; in this case, the server has to push updates quite frequently.
  * Pushing is cheaper but not real-time.
* Hybrid
  * We can adopt a hybrid approach. 
  * We can move all the users who have a high number of follows to a pull-based model and only push data to those users who have a few hundred (or thousand) follows. 
  * Another approach could be that the server pushes updates to all the users not more than a certain frequency, letting users with a lot of follows/updates to regularly pull data.

### Long polling vs polling
* Polling
  * Clients periodically check with the server if there are any changes. 
  * The problem with this approach is that we will have a delay in reflecting changes locally as clients will be checking for changes periodically compared to a server notifying whenever there is some change. 
  * If the client frequently checks the server for changes, it will not only be wasting bandwidth, as the server has to return an empty response most of the time, but will also be keeping the server busy. 
  * Pulling information in this manner is not scalable.
* Long polling 
  * With long polling the client requests information from the server with the expectation that the server may not respond immediately. 
  * If the server has no new data for the client when the poll is received, instead of sending an empty response, the server holds the request open and waits for response information to become available. 
  * Once it does have new information, the server immediately sends an HTTP/S response to the client, completing the open HTTP/S Request. 
  * Upon receipt of the server response, the client can immediately issue another server request for future updates.

### Long polling vs Server send event

### Server send events vs websocket connection 

### Websocket: permanent via health check vs re-establish connection

### DNS: Single vs multiple domain

### DNS: How to determine routing strategy

### Load balancer: How to determine which service is up or down
* Benefit of Loadbalancer approach is if a server is dead, LB will take it out of the rotation and will stop sending any traffic to it. 
* A problem with Round Robin LB is, it won’t take server load into consideration. 
* If a server is overloaded or slow, the LB will not stop sending new requests to that server. 
* To handle this, a more intelligent LB solution can be placed that periodically queries backend server about their load and adjusts traffic based on that.

### Load balancers vs API Gateway

### Load balancers vs reverse proxy

### Load balancers: Software vs Hardware 

### Load balancer: Layer 4 vs Layer 7 

### Load balancer algorithm

### Load balancers: Single vs multiple 

### Service: Monolith vs microservice

### Service: Handle race conditions

### Service: what would users see when computation is running
* Stale content
* No content available

### Service: In-memory computation or storage

### Service: Historical data might impact performance
* Before fetching the rows, clean the records based an expired time
* Use the callback functionality of redis when a key expires.
  * Not always precise as redis runs a background process to check for key's expiry time.
  * Less expensive
* poll a redis's delayed queue (based on the expiry timestamp) every 1 second, when the message is available, clean the record
  * More precise
  * Comes at a cost

### Service: Push vs pull vs in-process

### Service: APIGateway vs custom service
### In-house vs open source vs managed

### Service: Ambassador service vs service proxy for cross-cutting concerns

### Service: Pre-compute or compute-on-the-fly

### Process requests/events in order or un-ordered manner

### Service: Routing - based on what should we split data


### Service: Routing - who should be routing the data
* Software load balancer in front of our servers; that can map each UserID to a server to redirect the request.

### Server: Single vs multi-threaded processing

### Server: Multi-threaded- Serial vs parallelism vs concurrency
* Parallelism is when you can execute independent tasks in parallel.
  * Generating a sequence number can be parallelized by two server/threads
    * One generates even number
    * Other generates odd number
* Concurrency is when you protect the critical section access from multiple-threads

### Server: Multi-threaded - Blocking vs Non-blocking IO
* Blocking IO
  * Single thread per connection request
  * Easier to debug by looking at the thread stack.
* Non-Blocking IO
  * Requests are placed in a queue and processed as and when threads are available.
  * Actual I/O is processed at some later point.
  * More efficient and lesser throughput.

### Service: Computation on the fly errors

### Ensure idempotency: Same data is returned always

### Database: Consistency vs Availability
* Consistency
  * Ensure consistency in read.
  * Moment we have SQL replicas, caches, reads will become eventual consistent
  * Replication consistency techniques
    1. Eventual Consistency
    2. Relaxing Durability
      1. Relaxed-durability databases trade the full durability of committed transactions for enhanced runtime performance for transactional workloads.
      2. A relaxed-durability database created with the no_recovery level is similar to an in-memory database: you cannot recover data or logs if the server terminates or is shut down.
    3. Quorums
    4. Read-your-writes
      1. update request would generate a commit token
      2. replica which services the read request would use that commit token to determine whether it can service the read operation
      3. replica is current enough, it can immediately execute the transaction and satisfy the request.
      4. replica is not current enough
        1. replica takes if it is not consistent enough to service the read request is up to you as the application developer.
        2.  You can do anything from blocking while you wait for the transaction to be applied locally, to rejecting the read request outright.
* Availability

### Database: SQL vs NoSQL
* use SQL - Data is structured atleast and need ACID
* Use NoSQL - Document datastore - Data is semi-structured and schema changes often
* Use NoSQL - Columnar DB - Ever increasing data + finite queries

### Database: ACID vs BASE
* ACID
  * Atomicity
    * Transaction needs to be completed in full.
      * Partial transaction breaks atomicity.
    * All or nothing
    * No "partial" updates
    * Atomicity requires rolling back
      * Rolling back requires preventing dirty writes.
    * Classic example: Bank money transfer
  * Consistency
    * Consistency at data level
    * Every system should have the same value at any given time.
    * Data can span multiple state locations
    * Data needs to be consistent everywhere
    * Moving the database from one state to another
    * Constraint checks
      * "Referential integrity" - all references are consistent
      * column types
      * column length
      * column nullability
      * unique key constraints
  * Isolation
    * Every database transaction is run in its own "space"
    * No interference between transactions
    * Multiple transactions might need to work on the same data at the same time!
    * One needs to wait for the others
  * Durability
    * Data should be not be lost when there is a failure.
    * what's written stays written!
    * Read after write consistency (Linearizability)
    * Example: Read + modify race conditions
    * Durability techniques:
      * Write ahead log
        * Writing a lot of data to disk is expensive (indexes, data files, columns, rows, etc)
        * DBMSs persist a compressed version of the changes known as write-ahead-log segment (WAL)
      * Asynchronous snapshot
      * Append only files
* BASE
  * Eventual Consistency

### Database: Row vs column oriented
* Row oriented databases
  * Tables are stored as rows in disk
  * Single block IO read to table fetches multiple rows with all their columns
  * More IOs are required to find a particular row in a table scan
  * Once you find the row you get all the columns for that row.
  * OLTP
  * Optimal for read/writes
  * Compression isn't efficient
  * Aggregation isn't efficient
  * Efficient queries with multiple columns
* Column oriented databases
  * Tables are stored as columns in disk
  * Single block IO to the table fetches multiple columns with all the matching rows
  * Less IOs are required to get more values of a given column
  * Working with multiple columns require more IOs
  * OLAP
  * Writes are slower
  * Compress greatly
  * Aggregation is efficient
  * Inefficient queries with multiple columns

### Database save disk costs
* Differential updates

### Object storage: hot or cold
### Object storage: Do you need to encrypt file or not

### Cache stampede or thundering herd or cache miss attack
* Problem
  * refers to the scenario where data to fetch doesn't exist in the database and the data isn’t cached either. 
  * So every request hits the database eventually, defeating the purpose of using a cache. 
  * If a malicious user initiates lots of queries with such keys, the database can easily be overloaded.
* Solution 1
  * Cache keys with null value. Set a short TTL (Time to Live) for keys with null value.
* Solution 2
  * Using Bloom filter. A Bloom filter is a data structure that can rapidly tell us whether an element is present in a set or not. 
  * If the key exists, the request first goes to the cache and then queries the database if needed. 
  * If the key doesn't exist in the data set, it means the key doesn’t exist in the cache/database. 
    * In this case, the query will not hit the cache or database layer.

### Cache overhead in updating the stale content

### Cache/Database: Optimized for querying vs writing

### Cache placement
* Client
* DNS 
* APIGateway
* In-memory application
* Before database

### Cache updates
* Read data from the system:
  * Cache aside 
    * Steps
      * Application read from cache
      * Cache miss
      * Application read from database
      * Application get the data
      * Application update cache
    * When to use?
      * A cache doesn't provide native read-through and write-through operations. 
      * Resource demand is unpredictable. This pattern enables applications to load data on demand. It makes no assumptions about which data an application will require in advance.
    * When not to use?
      * When the cached data set is static. If the data will fit into the available cache space, prime the cache with the data on startup and apply a policy that prevents the data from expiring. 
      * For caching session state information in a web application hosted in a web farm. In this environment, you should avoid introducing dependencies based on client-server affinity.
  * Read through 
    * Application read from cache
    * cache miss
    * Cache reads from DB
    * Cache gets the data
    * Updates the cache
* Write data to the system:
  * Write around 
    * 
  * Write back 
    * Application writes to cache constantly
    * Write to DB once in a while
  * Write through
    * Application writes to cache
    * Cache writes to DB immediately

### Cache eviction policies
* Least recently used (LRU)
  * Discard the least recently used chunk first.
* Least frequently used

### Cache: Memory vs latency
* More memory less latency as you can cache a lot of things and reduce round trips to database.
* More memory would be expensive

### CDN content authorization checks
### CDN Overhead in updating the content
### CDN vs microservice reads
### CDN: push vs pull
### CDN: Local vs global
### Consistency: Strong vs eventual

### Consistency: Single vs distributed transaction


### Single transaction: Pessimistic vs Optimistic concurrency control
* Transaction block to execute multiple statements in a database
* Control Concurrency
  * Conflict Ignored
    * Last in-win solution
      * whoever writes last will override the previous request
    * Serialized requests
      * VoltDB and Redis are in-memory, single-threaded and guarantees serializability
  * **Pessimistic Concurrency Control** (Conflict avoidance)
    * Row level locks, table locks, page level locks to avoid lost updates
    * When to use: More number of conflicts
      * Preferred when there are lot of updates on the same row.
    * Types
      * Exclusive Lock
        * Prevent reads and writes
        * When there is a exclusive lock,
          * shared locks are not allowed
          * exclusive lock is not allowed
        * `SELECT FOR UPDATE` statement to lock a single row
          * Bad in terms of performance when we lock multiple rows as it could lock the entire table
        * `INSERT` also acquires an exclusive lock.
        * Create a lock table and lock on a single row uniquely to identify a set of rows on the main table.
      * Shared Lock
        * Allow reads, Prevent writes
        * When there is a shared lock,
          * other shared locks are allowed
          * exclusive lock is not allowed
        * `LOCK IN SHARE MODE`
    * Key lookup in redis
    * 2 phase locking
      * Expanding phase: Acquire locks, release no locks.
      * Shrinking phase: Release all locks, no further lock acquisition
      * Reads acquire shared locks
      * Writes acquire exclusive locks
  * **Optimistic Concurrency Control** (Conflict detection)
    * Higher performance than pessimistic locking when the updates are relatively low.
    * No locks, just track if things changed and fail the transaction if so.
    * When to use: Less number of conflicts
    * Multi-version Concurrency Control (MVCC)
      * Readers don't block writers and writers don't block readers
      * Writers block writers to prevent dirty writes.
    * Version based optimistic locking
      * ```sql UPDATE post SET name =`name`, version = 1 where id =1 and version=0 ```
      * Pros:
        * Prevents lost updates
      * Cons
        * Updating individual columns is a problem as your lock is dependent on version.
          * Solved by decomposing tables where each table would have a separate version column.
    * Versionless based optimistic locking
      * Instead of version, use the actual value of the column that needs to be updated.
      * Isolation level should be atleast read-committed and database should refresh a change.
    * Timestamp based concurrency control
    * Hash or checksum based concurrency control
    * Snapshot types
      * Query level: read committed
      * Transaction level: Snapshot isolation

### Single transaction: Isolation levels
* Problems
  * Dirty writes: Reading an uncommitted transaction
  * Non-repeatable read: Consecutive reads results in different values
    * In a transaction, reading a single row and sum of row should yield correct values
  * Phantom reads: Non-repeatable reads on multiple rows
    * Run a query based on a range
    * New row is inserted
    * Re-run the query on a range would yield a different result.
  * Read skew:
    * Alice reads table1-row1
    * Bob updates table1-row1 --> table1-rowupdate1, table2-row1 --> rable2-rowupdate1
    * Alice reads table2-rowupdate1 which is not related to table1-row1
  * Write skew:
    * Alice reads table1-row1-col1
    * Bob reads table1-row1-col2
    * Alice updates table1-row1-col1 --> table1-row1-colupdate1
    * Bob updates table1-row1-col2 --> table1-row1-colupdate2
    * table1-row1-colupdate1 and table1-row1-colupdate2 are not related
  * Lost update:
    * Overwrite a change without being aware of another change that happened.
    * Read, write a change,
      * over-written by another transaction,
      * read would result in a lost update.
* Serializable:
  * Transactions run as if they are serialized one after another.
  * Don't want others writing and reading
  * Implemented with optimistic concurrency control
  * Implemented with pessimistic SELECT FOR UPDATE
  * Dirty Read: NO, Non-repeatable read: NO,
  * Phantom read: NO, Read Skew: NO
  * Write Skew: NO, Lost Update: NO
* Snapshot
  * Each query in a transaction only sees changes that have been committed up to the transaction.
    * It's like a snapshot version of the database at the moment.
  * Dirty Read: NO, Non-repeatable read: NO,
  * Phantom read: NO, Read Skew: NO
  * Write Skew: NO, Lost Update: NO
* Repeatable read:
  * Transaction will make sure that when a query reads a row,
    * that row will remain unchanged the transaction while its running.
  * Locks the row it reads but it could get expensive if you read a lot of rows
    * PostGres implements RR as a snapshot
    * That is why there is no phantom reads in PostGres.
  * Dirty Read: NO, Non-repeatable read: NO,
  * Phantom read: NO, Read Skew: NO
  * Write Skew: YES, Lost Update: NO
* Read committed:
  * Each query in the transaction only sees committed changes by other transactions.
  * Dirty Read: NO, Non-repeatable read: YES,
  * Phantom read: YES, Read Skew: YES
  * Write Skew: YES, Lost Update: YES
* Read uncommitted:
  * No isolation, any change from outside is visible to the transaction, committed or not.
  * Dirty Read: YES, Non-repeatable read: YES,
  * Phantom read: YES, Read Skew: YES
  * Write Skew: YES, Lost Update: YES

### Distributed transaction: Conflict ignored vs avoidance vs detection
* Conflict Ignored
  * **Sticky sessions**
    * Avoid race conditions by forwarding requests to same node or region.
* Conflict avoidance
  * **Two phase commit**
    * Strong consistency
    * Prepare Phase is successful and then during Commit phase one of the parties cannot commit it,
      * the coordinator retries that.
    * Phase
      * Prepare phase
      * Commit phase
    * Pros
      * Each microservice is responsible for rollbacks
    * Cons
      * Latency issues
      * Resources is blocked and no one has access to these resources
      * Microservice can fail to reply during different phases
      * Orchestrator/Coordinator can be a single point of failure.
      * Chatty: At least O(4n) messages, with O(n^2) retries
      * Not supported by many NoSQL databases
      * CAP theorem --> 2PC impacts availability
      * Network issues with distributed instances (partitions)
      * overhead to ensure consistency
  * **Three phase commit**
    * Much better than two-phase commit
    * Easier to recover on microservice or orchestrator failure
      * As any participant can become a co-ordinator
    * Phases
      * Collect votes: Can commit
      * Commit Authorized: pre-commit
      * Finalize commit: do-commit
  * **eventual consistency (vector clock + RWN)**
  * **Paxos**
  * **In-Sync Replica**
* Conflict detection
  * **SAGA**
    * Every transaction has a compensating rollback transaction.
    * Request issues a SAGA. When to send back a response?
      * Response specifies the outcome i.e. completion of SAGA
        * Reduces availability i.e. all services needs to be running.
      * Response specifies the SAGA initiation and outcome sent asynchronously.
        * Improved availability
        * Client must be notified or polled.
    * Pros:
      * Asynchronous pattern
      * Developer must write application logic to "rollback" eventually consistent transactions
    * Cons:
      * Careful design required
    * Orchestrator pattern
      * Centralized decision making
      * Orchestrator takes care of the calling the next microservice and also rollbacks.
      * Types
        * Implicit orchestrator
          * Existing domain object e.g. order aggregate
          * As soon as it receives an order request, order event is published.
          * Order is created only when it is approved or rejected.
          * Pros: Simple
          * Cons: Bloated responsibilities
        * Explicit orchestrator
          * Dedicated object
          * As soon as it receives an order request, order state is created in the database.
          * Requests are made to services.
          * Pros: Improved separation of concerns
          * Cons: Additional class
    * Choreography pattern
      * Distributed decision making
      * Each microservice is kicked-off based on an event happening.

### Sharding: Data suitability

### Sharding: How to avoid hot shards
* Use timestamp to send the data to same partition for a while to equally spread data
* Create multiple partition for hot users using composite keys
* Create a new range for hot keys in consistent hashing algorithms.

### Shard: outage affecting a set of users

### Sharding: routing at application layer vs external proxy

### Sharding: partitioning strategy - based on what should we split the data
* List based partitioning
  * sharding logic implements a map that routes a request for data to the shard that contains that data using the shard key.
  * Offers more control over the way that shards are configured and used. 
  * Using virtual shards reduces the impact when rebalancing data because new physical partitions can be added to even out the workload. 
  * The mapping between a virtual shard and the physical partitions that implement the shard can be modified without affecting application code that uses a shard key to store and retrieve data. 
  * Looking up shard locations can impose an additional overhead.
  * Example: Created timestamp, User/Customer
* Range based partitioning
  * Strategy groups related items together in the same shard, and orders them by shard key—the shard keys are sequential.
  * Useful for applications that frequently retrieve sets of items using range queries (queries that return a set of data items for a shard key that falls within a given range).
  * This is easy to implement and works well with range queries because they can often fetch multiple data items from a single shard in a single operation. 
  * This strategy offers easier data management. 
  * For example, if users in the same region are in the same shard, updates can be scheduled in each time zone based on the local load and demand pattern. 
  * However, this strategy doesn't provide optimal balancing between shards. 
  * Rebalancing shards is difficult and might not resolve the problem of uneven load if the majority of activity is for adjacent shard keys.
  * Example: 
  * Problem: Overloaded partition
* Hash based partitioning
  * Can take the hash of the ‘FileID’ of the File object we are storing to determine the partition the file will be stored. 
  * Our hashing function will randomly distribute objects into different partitions, 
  * e.g., our hashing function can always map any ID to a number between 1…256, and this number would be the partition we will store our object. 
  * This strategy offers a better chance of more even data and load distribution. 
  * Request routing can be accomplished directly by using the hash function. 
  * There's no need to maintain a map. Note that computing the hash might impose an additional overhead. 
  * Also, rebalancing shards is difficult.
  * Example: 
  * Problem: Overloaded partition

### Sharding: Once sharded how do you find the shard
* We can append the shardId to the resource id
  * Bottleneck: 
    * Would be to redirect resource when it is migrated from one shard to another.
  * Each shard can have its own sequence number
* Hash modulo: ShardId mod (number of shards)

### Sharding: Logical vs physical
* Multiple logical partitions reside on a single physical database server
* Maintain a config file (or a separate database) that can map our logical partitions to database servers; this will enable us to move partitions around easily.

### Sharding vs read-replicas
* Sharding
  * Shard when the DB size (with same tables) is in the range of TB
    * Different tables it is better to perform functional decomposition.
  * Complicated to implement. Several decisions on where query routing needs to be placed i.e. application layer or separate proxy.
* Read-replicas
  * Simple to implement.
  * Except the reads to have slight lags.

### Database: Horizontal vs vertical partitioning
* Horizontal partitioning vs sharding
  * Preferred when there the data is same. 
* Vertical partitioning vs functional decomposition
  * Partition our database in such a way that we store tables related to one particular feature on one server.
  * For example, we can store 
    * all the user related tables in one database 
    * all files/chunks related tables in another database
  * Preferred when there are different data to be chunked.

### Database: Performance in joining tables across distributed databases
* How frequently do we need to join tables?

### Consistency: Handle partial failures
* write-off: On failure, Can't proceed with the distributed transaction
* retry: On failure, try to perform the same action again
* Compensating action: On failure, try to do an alternate action

### Availability: Single point of failure

### Replication vs consensus

### Consensus algorithm


### Availability: Replication encoding scheme
* Mirroring: Store multiple copies of the data on different servers
* Use techniques like Reed-Solomon encoding to distribute and replicate it.

### Replicas: Synchronous vs Asynchronous replication in SQL databases
### Replicas: Synchronous - writes to master or all replicas

### Leader selection algorithm
* Selecting the task instance with the lowest-ranked instance or process ID.
* Racing to acquire a shared, distributed mutex. The first task instance that acquires the mutex is the leader. However, the system must ensure that, if the leader terminates or becomes disconnected from the rest of the system, the mutex is released to allow another task instance to become the leader.
* Implementing one of the common leader election algorithms such as the Bully Algorithm or the Ring Algorithm. These algorithms assume that each candidate in the election has a unique ID, and that it can communicate with the other candidates reliably.

### Database: Handle inconsistency issue with multiple masters
* Code can decide based on the timestamps
* Rollback inconsistent data
* Ask the user to resolve inconsistencies

### Leaderless replication: choice for coordinator node
### Leaderless replication: Number of quorum reads vs writes
### Service discovery: Client vs server side
### Service discovery: where to place
### Resiliency: Load shedding vs managing load
### Resiliency: Automatic vs manual
### Resiliency client: drop or retry failed requests
### Resiliency client: Retry requests - Exponential backoff vs jitter to avoid retry storm
### Resiliency client: Timeout vs circuit breaker
### Resiliency client: Timeout - Connection and request timout values
### Resiliency client: Circuit breaker - Error threshold vs timeouts

### Priority queue topology

### Priority queue: preempt or continue processing a low priority message when a high priority message arrives

### Upgrade message priority dynamically or not

### Messaging: Queue messages that end up in failure
### Messaging: Queue messages that can't be processed

### Messaging: Queue messages that can be duplicated

### Messaging: Queue messages expiry time


### Messaging: Queue messages to be grouped
* When multiple receivers retrieve messages from a queue, there is usually no guarantee over which receiver handles any specific message. 
* Messages should ideally be independent. 
* However, there may be occasions when it is difficult to eliminate dependencies, and it may be necessary to group messages together so that they are all handled by the same receiver.

### Messaging: Queue messages to be scheduled
* A message might be temporarily embargoed and should not be processed until a specific date and time. 
* The message should not be available to a receiver until this time.

### Messaging: When the entire queue cluster is not available

### Consumer: Single vs multiple consumer for queues

### Messaging: Checkpointing - Commit individual or group of messages
### Messaging: Partition the queue or not
* Have separate partition based on 
  * Hash of something
    * Easier to partition.
    * Would end up in hot partitions
  * Every client
    * Overhead of creating partition for new clients
    * No overhead in processing when the client is offline

### Publisher or load balancer distributing messages to different queues/partitions

### Messaging: Publisher need or need not decide on partitioning strategy

### Messaging: Subscription pattern
* Wildcard subscribers: Consider allowing subscribers to subscribe to multiple topics via wildcards.
* Subsets of messages. Subscribers are usually only interested in subset of the messages distributed by a publisher.
  * Topics. Each topic has a dedicated output channel, and each consumer can subscribe to all relevant topics. 
  * Content filtering. Messages are inspected and distributed based on the content of each message. Each subscriber can specify the content it is interested in.

### Messaging: Single vs multi-threaded consumer
### Analytics: Batch vs stream vs both
### Analytics: Batch processing - What is our batching strategy

### Communication patterns
* Request/Response
  * Synchronous + Pull/Push data
* Long polling
  * Synchronous + Pull data
* Streaming over persistent connections
  * Synchronous + Push/Pull data
  * Modes
    * Server to client - Example: video streaming
    * Client to server - Example: File upload
    * Bidirectional - Example: Gaming
* Webhooks
  * Asynchronous + Push data
* Callbacks
  * Asynchronous + Push data
* Broadcast to all clients
* Gossip communication among clients - De-centralization
  * Asynchronous + Push data

### Communication Messaging formats
* JSON
  * Unstructured data
  * No way to validate schema
  * Take a lot more size compared to protobuf
* XML
* CSV
* Kyro
  * very fast, very compact, but it works only on JVM
* Remote procedure call
  * Protobuf
    * Structured data
    * Has a well-defined schema
    * Format used for event-driven message-brokers
    * Serialized data is of a very small size compared to JSONs.
    * Easy to create language libraries from protobuf spec.
    * Con: Not human-readable
    * Con: Dependency on protobuf compiler
  * AVRO
    * Schema is written in JSON or IDL
    * Format used for event-driven message-brokers
  * Thrift

### Communication architecture style
* REST
  * Message format: XML, JSON
  * No schema required
  * Need to choose from multiple custom HTTP libraries
* GraphQL with REST
* Apache parquet
  * column-oriented data storage format of the Apache Hadoop ecosystem
* RCFile
* ORC
* gRPC
  * One library for popular languages
  * All requests are stateful i.e. tagged with a streamId.
  * Protocol: HTTP/2
  * Message format: protobuf
  * Modes of communication
    * Unary RPC - Request response
    * Server streaming RPC - Stream from server
    * Client streaming RPC - Stream from client
    * Bidirectional streaming RPC - Stream bidirectionally
  * Pro: Fast and compact
  * Pro: Progress feedback (Upload)
  * Pro: Cancel Request (H2)
  * Con: Schema
  * Con: Thick client. Needs to be updated.
  * Con: Service proxies compatibility is missing
  * Con: Still young (support)
  * Con: Error handling. No HTTP codes supported.
  * Con: No native browser support
  * Con: Timeouts management
* Hermes
  * Implemented by Spotify.
  * Spotify later moved to gRPC.

### Communication protocols
* SOAP
  * Message format: XML
  * Need to choose from multiple custom HTTP libraries
* Server send events
  * Synchronous + push data from server to client
  * Client - GET text/event-stream /api on initial request
  * Server - SSE response text/event-stream
* Websockets
  * Synchronous + push data
  * Build on top of TCP
  * Low latency, No lag
  * Bidirectional communication protocol
  * Client - HTTP GET 1.1 UPGRADE on initial request
  * Client requests some data on the next call
  * Server would send the updates as response
* RSocket
* Raw TCP
  * Synchronous
* Java serialization

### Communication Spec
* Software
  * Open Source: OpenAPI Spec
  * Commercial:
  * AWS:
  * Azure:
  * GCP:

### OSI Layer protocols
* **Application Layer**
  * HTTP is in the application layer and normally TCP based, since HTTP assumes a reliable transport.
  * Protocol
    * HTTP/HTTPs - Hypertext Transfer Protocol
    * BitTorrent - peer to peer file sharing
    * MIME - Multipurpose Internet Mail Extensions and Secure MIME
    * LDAP - Lightweight Directory Access Protocol
    * SSH - Secure Shell
    * XMPP - Extensible Messaging and Presence Protocol
* **Presentation layer**
* **Session Layer**
  * RPC, a session layer (or application layer in TCP/IP layer model) protocol, is an inter-process communication
    * that allows a computer program to cause a subroutine or procedure to execute in another address space (commonly on another computer on a shared network),
    * without the programmer explicitly coding the details for this remote interaction.
* **Transport Layer**
  * TCP - Transmission Control Protocol
    * TCP is reliable and connection-based.
    * TCP is the underlying protocol beneath HTTP
    * Transmission protocol
    * Layer 4 protocol
    * Client
      * Assigns packet number
      * Ensures packets are not lost
        * by retrying to send packet which are not ACK-ed
        * tracks ACK-ed packets
      * congestion control
        * delay sending packets
    * Server
      * arrange the received packets in order
  * UDP - User Datagram Protocol
    * UDP is connectionless and unreliable.
    * Layer 4 protocol
    * Client
      * keeps sending the payload irrespective of whether the server is receiving or not
      * Doesn't try to resend packets
* **Network Layer**
  * IP - Internet Protocol
    * IP is an unreliable protocol
    * Layer 3 protocol
    * Determine the physical path the data will take.
* **Data Link Layer**
  * ARP - Address Resolution Protocol
* **Physical Layer**

### Serialization vs Encoding vs Hashcode
* Serialization

* Encoding
  * Encoding is the process of putting a sequence of characters into a specialized format for efficient transmission or storage.
  * Decoding is the process of an encoded format into original sequence of characters

* ASCII
  * Letter maps to a byte which is 8 bits.
  * Ascii 32-47 represent characters such as space and so on
    * 48-57 represent characters 0-9
    * 58-64 represent characters such as :, ; and so on.
    * 65-90 represent A-Z
    * 97-122 represent a-z

* Unicode
  * Ways to encode unicode characters to byte sequences.
  * Single character set that included every reasonable writing system.
  * Letter maps to code point.
    * English letter A would be U+0041.
  * Different encoding formats
    * UTF-16
      * Represent unicode in 16 bits words where each character is represented in 16 bits.
    * UTF-8
      * Represent in 8 bits and matches the ASCII code. Makes it easier for american character set.
      * Other languages which have more than 128 bits are represented in 2 to 6 bytes.
  * All developers should be using Unicode instead of ASCII to support internalization.

* Base-encoding
  * Encode a byte sequence (String) to a string of fixed characters.
  * Base36: a-z, 0-9
  * Base62: A-Z, a-z, 0-9
  * Base64: A-Z, a-z, 0-9, -, .
    * Number of unique strings
      * Number of possible 6-character strings: 64^6 ~= 68.7 billion
      * Number of possible 8-character strings: 64^8 ~= 281 trillion
    * Base64 character encodes 6 bits
      * 128 bit encoding would result in nearly 21 characters.

* Hash Coding
  * Convert a string of characters into a shorter fixed length value of key that represent the original string.
  * MD5:
    * Produces 128-bit hash value
  * SHA256

### Interface vs schema
* Interface
```java
public interface AppManager {

    String createApp(App app);
    void deleteApp(String id);
    boolean updateApp(String id, App app);
}
```
* App is the schema
```java
public class App {
    private String id;
    private String name;
}
```

### Private vs public IP address
* NAT is responsible for translating public address to private address

### Kubernetes vs virtual machines

