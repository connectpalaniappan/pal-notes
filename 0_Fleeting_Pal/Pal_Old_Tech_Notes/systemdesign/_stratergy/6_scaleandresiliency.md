Scale is about adding to your basic cloud architecture so that it can handle more than a handful of users.

1. [Scalability](#scalability)
   1. [Functional decomposition](#functional-decomposition)
      1. [Microservices](#microservices)
      2. [CQRS](#cqrs)
      3. [Coordination and Service discovery](#coordination-and-service-discovery)
      4. [Service proxy](#service-proxy)
      5. [Service mesh](#service-mesh)
      6. [APIGateway](#apigateway)
      7. [scheduling and orchestration](#scheduling-and-orchestration)
   2. [Duplication](#duplication)
      1. [Horizontal Scaling](#horizontal-scaling)
      2. [Network load balancing](#network-load-balancing)
      3. [Reverse proxy](#reverse-proxy)
      4. [Caching](#caching)
      5. [Content Delivery network](#content-delivery-network)
      6. [Replication](#replication)
         1. Types
            1. [Single-leader](#single-leader-replication)
            2. [Multi-leader](#multi-leader-replication)
            3. [Leaderless](#leaderless-replication)
      7. [Multiple Region](#multiple-region)
         1. [Replication](#replication)
   3. [Partitioning](#partitioning)
      1. [Sharding](#sharding)
      2. [Re-balancing](#re-balancing)
2. [Resiliency](#resiliency)
   1. [Upstream resiliency - Server](#upstream-resiliency-server)
       1. [Load shedding](#load-shedding)
       2. [Load leveling](#load-leveling)
       3. [Rate limiting](#rate-limiting)
       4. [Bulkhead](#bulkhead)
       5. [failover]()
          1. [active-passive service/database failover]()
          2. [Multiple region/availability zone failover](#multiple-region)
       6. [Extra capacity ahead]()
       7. [Autoscaling]()
       8. [Managed service]() - High availability
       9. [Health endpoint](#health-endpoint) - load balancer redirects
       10. [Watchdog](#watchdog)
   2. [Downstream resiliency - Client](#downstream-resiliency-client)
       1. [Timeouts](#timeouts)
          1. [Adaptive reconnect timeouts](#timeouts)
       2. [Retry - Exponential Backoff](#retry---exponential-backoff)
       3. [Retry amplification](#retry-amplification)
       4. [Circuit breaker](#circuit-breaker)
       5. [Automatic failover]() 
3. [Performance](#performance)
   1. [Server]()
      1. [Request Processing]()
   2. [Client]()
      1. [Request Buffering and Batching]()

## Scaling based on users
* 1-10 users
  * Single application and database server
* One hundred users
  * Separate database server - sql vs nosql
* One thousand (1k) users
  * Horizontal or vertical scaling (duplication)
  * load balancer (duplication)
  * database replication (duplication)
  * read replicas (duplication)
  * multiple masters (duplication)
* Ten thousand (10k) users
  * caches (duplication)
  * content delivery network (duplication)
* Hundred thousand (100k) users
  * stateless vs stateful web tier
    * Moving session information to caches (functional decomposition)
* Five hundred thousand (500k) users
  * multiple datacenter (duplication)
  * geoDNS (duplication)
* 1 million (1,000,000) users
  * Message queue (functional decomposition)
  * Logging, metrics and automation 
* Ten million (10,000,000) users
  * database sharding (partitioning)
  * vertical partition by functionality (functional decomposition)
  * Move some functionality to NoSQL (functional decomposition)

## Scalability 

### Functional decomposition

#### Microservices

#### CQRS

#### Coordination and Service discovery
* Service discovery tools address this problem by providing a common place to find and potentially identify individual services. 
* There are basically two types of tools in this category:
  * Service discovery engines: database-like tools that store information on all services and how to locate them 
  * Name resolution tools: tools that receive service location requests and return network address information (e.g. CoreDNS)
* Used to identify the active instances
* Health connection checks to instances
* Instances with name, address, port, etc. are registered into the path in ZooKeeper for each service. 
  * If one service does not know where to find another service, it can query Zookeeper for the location and memorize it until that location is unavailable.
* Zookeeper is a CP system in terms of CAP theorem
  * which means it stays consistent in the case of failures, but the leader of the centralized consensus will be unavailable for registering new services.
* In contrast to Zookeeper, Uber is doing interesting work in a decentralized way, named hyperbahn, based on Ringpop consistent hash ring.
* Software
  * Open Source: CoreDNS, Etcd, Zookeeper, Netflix Eureka, k8GB, Nacos
  * Commercial:
  * AWS: AWS CloudMap
  * Azure:
  * GCP:

#### Service proxy
* Service proxy is a tool that intercepts traffic to or from a given service, applies some logic to it, 
  * then forwards that traffic to another service.
* can be as simple as serving as a load balancer that forwards traffic to individual applications or 
  * as complex as an interconnected mesh of proxies running side by side with individual containerized applications handling all network connections.
* Centralizing the distribution and management of globally needed service functionality such as routing or TLS termination from a single common location 
  * allows communication between services to become more reliable, secure, and performant.
* Responsibilities
  * Server-side encryption
  * TLS (SSL) termination
  * Response compression
  * caching web acceleration
  * canary deployment
  * publish metrics
  * manage routing (spreading traffic evenly among services or rerouting if some services break down)
* Software
  * Open Source: Envoy, HAproxy, Zuul, Nginx, Traefik proxy, Contour
  * Commercial:
  * AWS:
  * Azure:
  * GCP:

#### Service Mesh
* Service meshes manage traffic (i.e. communication) between services. 
* They enable platform teams to add reliability, observability, and security features uniformly across all services running within a cluster without requiring any code changes.
* Service meshes bind all services running on a cluster together via service proxies creating a mesh of services, hence service mesh.
* These are managed and controlled through the service mesh control plane. 
* Service meshes allow platform owners to perform common actions or collect data on applications without having developers write custom logic.
* Enhances application-to-application connectivity through policies
* Controls the east-west traffic i.e. traffic between services
* Software
  * Open Source: Consul, Istio, Linkerd, Traefik Mesh
    * Open service mesh, Meshery, Kuma
  * Commercial:
  * AWS: AWS App Mesh
  * Azure:
  * GCP:

#### APIGateway
* API gateway allows organizations to move key functions, such as authorizing or limiting the number of requests between applications, to a centrally managed location.
* API gateway sits between the users and the application
* Responsibilities
  * Inbound connectivity to an environment
  * Controls the north-south traffic i.e. traffic from external users.
  * Converts message format between internal and external systems
  * Global and service level policies enforcement
  * Monitor SLAs
  * Cache service responses
  * Rate-limiting
  * Auditing
* Software
  * Open Source: Kong, Sentinel, Mulesoft, Kusk, KrakenD
  * Commercial:
  * AWS:
  * Azure:
  * GCP:

#### Scheduling and orchestration

### Duplication

#### Network load balancing
* Route the requests by distributing traffic
* Software vs Hardware
* Knows explicitly the domain name or IP address of the machines.
* monitor instance health
* Can be in-front of application, databases
* Secondary LB by monitoring primary LB takes over when primary is impacted
* Type of load balancers
  * DNS load balancing
    * Domain name to determine which load balancer to forward requests to.
    * pros: easy to implement and free 
    * cons: hard to control and not responsive, since DNS cache needs time to expire
  * Transport layer load balancing - L4 layer
    * TCP does not terminate connection and handles million of requests per second
    * traffic is routed by IP address and port
    * pros: better granularity, simple, responsive.
  * Application layer load balancing - L7 layer
    * HTTP connection is established every time.
    * Load balancer HTTP algorithms - 
      * Round robin, least connection, least response time, hash based,
      * least loaded, least loaded with slow start, utilization limit, latency, cascade,
  * Geo load balancing
* Where to place a load balancer?
  * Between Clients and Application servers 
  * Between Application Servers and database servers 
  * Between Application Servers and Cache servers
* Software
  * Open Source: HAProxy, Nginx, Netscaler(hardware)
  * Commercial:
  * AWS: Amazon Elastic load balancer
  * Azure:
  * GCP:

#### Reverse proxy
* Reverse proxy centralizes internal services and provides unified interfaces to the public.
* Load balancer is a special kind of reverse proxy
* all functionalities of load balancer +
* caching
* Software
  * Open Source: Varnish
  * Commercial:
  * AWS:
  * Azure:
  * GCP:

#### Horizontal Scaling

#### Caching
* Policies
* In-process cache
* Out-of-process cache
* Cache - Files - Content delivery network
  * Spread geographically
  * Local CDNs can share files among themselves, thereby decentralizing the asset download process.
* three major factors to consider when we design the cache.
  * Pattern: How to cache? is it read-through/write-through/write-around/write-back/cache-aside? 
    * Read-Through
    * Write-Through
    * Write-Around
    * Write-back
    * Cache-aside
  * Placement: Where to place the cache?
    * Client side
    * Application side
    * Database side
  * Replacement: When to expire/replace the data? 
    * Least Recently used (LRU)
    * Least Frequently used (LFU)
    * ARC

#### Replication
##### Single-leader replication
  * SQL
    * Configuration service to determine health of primary/secondary replicas (master-slave)
    * Replication between master-slave
    * Read-replicas for reporting
      * Out of date content to be served, read requests can be scaled
    * Vitess to auto-manage scaling
  * Different modes of stand-by
    * Cold standby
      * Cold standby systems are turned on once to install and configure the system and data and then turned off until needed. 
      * Thereafter, it's employed only when updating noncritical data, which is done infrequently, or on failure of the primary system.
    * Warm standby
      * a warm standby system runs in the background of the primary system and data is regularly mirrored to a secondary server. 
      * Therefore at times, the primary and secondary systems do contain different data or different data versions.
    * Hot standby
      * a hot standby system is running simultaneously with another identical primary system. 
      * On failure of the primary system, the hot standby system immediately takes over to replace the primary. 
      * In such a setup, the data is mirrored in real time and both systems have identical data.
##### Multi-leader replication
##### Leaderless replication
  * No-SQL
    * Gossip communication to share info about all nodes
    * Replication with adjacent nodes
    * Coordinator node would perform quorum reads/writes to decide on the correct value

#### Content-Delivery Network
* Companies would provide free hardware to ISPs to cache their content.
  * Netflix implements this optimization with a strategy called openconnect.
  * Placed before CDNs, it would reduce the load on CDNs.
  * Flow: modem -> router -> ISP's router -> local CDN -> main CDN -> S3

#### Multiple region
* Purpose
  * Split based on geography i.e. Asia-pacific vs US vs europe
  * Business continuity / disaster recovery
  * Geographically distributed databases
    * Improve latency for end-users
    * Legal and data regulatory compliance
  * Blue/Green deployment
* Strategy
  * Back & restore
    * Downtime: 24 hours
    * Data loss: hours
  * Pilot light (Active running-Passive not running)
    * Downtime: minutes to hours
    * Data loss: minutes
  * Warm-standby (Active running-Passive running)
    * Passive does not take traffic
    * Downtime: minutes
    * Data-loss: sub-second
      * Multi-phase commit: zero
  * Active running - Active running
    * Downtime: near zero
    * Data-loss: near zero
* Pattern
  * Read local and write global
    * Always write to a global i.e. main region
    * Due to synchronization, you can read from local region
    * Read:write ratio is 90-95%
    * Use case: User signup and authorization
  * Read local and write partitioned
    * Application code is sharded
    * Singapore user will always write to singapore region even when they access the system from Oregon.
    * Though they would read from their local region i.e. they fly to oregon, they would read from oregon region.
    * Read:write ratio is 50%
  * Read local and write local
    * Anti-pattern due to data collisions.
    * Multi-master and multi-region
* Implementation
  * Multi-region DNS routing
  * Read-Write
    * Master/Replica
    * Master/Master
  * Read-Only
    * Scheduled replication
    * Near real time eventual consistency from master copy
* Problems
  * Data collisions
* Network: Multi-region multi-VPC (private network) connectivity
* Routing: Latency, Geolocation, DNS failover, 
* Network load balancer: TCP Proxy-4

### Partitioning

#### Sharding
* Useful strategy when there are a lot of write requests
* Types
  * Sharding or range partition or horizontal partitioning
    * Pre-defined map of the object to the partition.
  * HashBased partitioning
    * Calculate the hash of the object
    * Randomly distribute hash into different partitions number say 1 to 256
    * Number would represent the partition in which we store the object
    * Approach will lead to overloaded partitions.
  * Modulo hash partitioning
    * Calculate the hash of the object.
    * Determine the correct partition by performing modulo operation of the hash object with the number of partitions. 
    * Approach will lead to overloaded partitions
  * Consistent hashing
    * Quorum 
      * Strong consistency: Reads replicas + write replicas > no. of replicas
    * Increased entropy: When one replica is out of sync with another
* Software
  * Google Cloud: Spinnaker

#### Re-balancing
* Static partitioning
* Dynamic partitioning
  
## Resiliency 

### Downstream resiliency (Client)

#### Timeouts
* Connection timeout - timeout when connection cannot be established
* Request timeout - timeout when request processing not completed
  * identified by p99.

#### Retry - Exponential backoff
* Avoid retry storm

#### Retry amplification
* Avoid retry storm by jitter algorithms

#### Circuit breaker
* Examples: Netflix Hystrix, Polly

### Upstream resiliency (Server)

#### Load shedding

#### Load leveling

#### Rate-limiting

#### Bulkhead
* Isolate elements of an application into pools so that if one fails, the others will continue to function. 
* This pattern is named Bulkhead because it resembles the sectioned partitions of a ship’s hull. 
* Partition service instances into different groups, based on consumer load and availability requirements. 
* This design helps to isolate failures, and allows you to sustain service functionality for some consumers, even during a failure.
* Thundering herd problem
  * When a flood of requests hit the application server and bring it down.
  * Cache the responses as much as possible to avoid overloading the database.
  * When there are multiple requests, process only one unique request before processing all the requests simultaneously.
  * When the unique request is cached, processing simultaneous requests should be easier.

#### Health endpoint

#### Watchdog

### Performance

#### Request Buffering and Batching
* On failure, do we send the entire batch or just the failed parts of the batch?

#### Request processing
* Blocking (one thread per connection)
* Non-blocking (single thread handling multiple connections by processing requests from queue)

