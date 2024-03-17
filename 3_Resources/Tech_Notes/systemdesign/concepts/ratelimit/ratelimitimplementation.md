Local and distributed rate limit https://youtu.be/FU4WlwfS3G0

### Algorithm
- Token bucket algorithm
  TODO

### Requirements

-  Why not scale the software that needs to handle load ?
- load balancer cannot differentiate requests. So not good to handle throttling in load balancer.
- What if we throttle on each host individually ?
  Load balancers distribute the request unevenly and application servers might be slow due to overload, so we need to throttle at a global level.
- Functional
    - allowRequest(request)
- Non-functional
    - Low latency (make decision as fast as possible)
    - Accurate (as accurate as we can get)
    - Scalable (Supports an arbitrary large number of hosts in the cluster)
    - high availability (not needed as we may not throttle when throttle service is not available)
    - fault tolerant (not needed as we may not throttle when throttle service results in failure)
    - Ease of integration

###  Building a solution
- Simple solution on one server
    - Rules database to store the rules to throttle
    - Rules Service - CRUD on rules database
    - Throttle rules retriever - communicates with client
    - Throttle cache - cache of throttle rules
    - Client identifier builder
    - Rate limiter component - checks the key against the cache
- three ways to handle rejection
    - drop the request
    - process the request later by placing in a queue
    - return a 429/503 error code
- Algorithm to implement
    - Google Guava ratelimiter class
    - token bucket algorithm

#### Object oriented design
- JobScheduler
    - Starts/stops scheduler (e.g. ScheduledExecutorService )
    - Run RetrieveRulesTask periodically
- TokenCache
    - Stores token bucket objects
        - Map/ ConcurrentHashMap/ Google Guava Cache
    - ClientIdentifier
        - Retrieves client identity information from request context
    - Ratelimiter
        - TokenBucketRateLimiter
            - Retrieves token bucket from cache
            - call allowRequest() on the bucket
- RetrieveRulesTask
    - Make a remote call to Rules service
    - Create token buckets and loads them into cache

#### System distributed design
- Sometimes more requests would be processed in a distributed system than what is expected. That should be fine.
- topology
    - Tell everyone everything
        - Options
            - 3rd party service to read heartbeats from every hosts
            - user specifies a vip where vip points to all the hosts
            - list of hosts via configuration file
        - not scalable
    - gossip communication
    - distributed cache such as redis
    - Coordination service
        - consensus service such as parox or raft can be used
    - Random leader selection
- protocol between hosts
    - TCP - more accurate and less faster due to error checking
    - UDP - less accurate and faster

### integrate with service
- library as a part of service process
- separate process in same host

### optimizations
- delete unused buckets to avoid memory space
- use thread safe classes such as atomic and concurrent hashmap instead of synchronized classes
- client can use exponential backoff and jitter for retries.

### scalability
- number of hosts in cluster
- number of rules
- request rate
- few thousand hosts - gossip over UDP is fast
- many thousand hosts - distributed cache is better but increases operation cost and latency.

### Reference
https://drive.google.com/file/d/1sr48lUIsVkb-I4rRyCtu2EtcudyfRoPD/view
