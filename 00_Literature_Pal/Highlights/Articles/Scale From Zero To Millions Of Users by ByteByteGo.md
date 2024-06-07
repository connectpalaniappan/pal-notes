---
title: Scale From Zero To Millions Of Users
full Title: Scale From Zero To Millions Of Users
author: ByteByteGo
URL: https://bytebytego.com/courses/system-design-interview/scale-from-zero-to-millions-of-users
published date: 
category: articles
source: reader
tags: [medium/articles, author/ByteByteGo, reader/reader, date/2024-05-01, area/reader]
created: 2024-04-30
assignedTo: people/pal
priority: P4
work: document
---
author:: [[ByteByteGo]]
note:: 
source:: [[reader]]
url:: [articles URL](https://bytebytego.com/courses/system-design-interview/scale-from-zero-to-millions-of-users)
image_url:: [articles image URL](https://bytebytego.com/social.png)
category:: [[articles]]
date:: [[2024-04-30]]
last_highlighted_date:: [[2024-05-01]]
published_date:: [[]]
summary:: The text discusses scaling a system from a single server setup to supporting millions of users through techniques like separating web and data tiers, database replication, and utilizing cache servers for improved performance and scalability. By following key principles like keeping the web tier stateless, building redundancy, caching data, and scaling the data tier through sharding, the system can handle high traffic loads and ensure reliability and availability for users across different regions. Additionally, the text highlights the importance of monitoring the system, utilizing automation tools, and hosting static assets in CDNs to optimize performance and support a large user base.


![rw-book-cover](https://bytebytego.com/social.png)

## Highlights
### id713607977
[[2024-04-30]] 18:42
> ![](data:image/svg+xml,%3csvg%20xmlns=%27http://www.w3.org/2000/svg%27%20version=%271.1%27%20width=%27500%27%20height=%27287%27/%3e)![Figure 2](https://bytebytego.com/_next/image?url=%2Fimages%2Fcourses%2Fsystem-design-interview%2Fscale-from-zero-to-millions-of-users%2Ffigure-1-2-GPY73ZNO.png&w=1080&q=75)
> Figure 2
> 1. Users access websites through domain names, such as api.mysite.com. Usually, the Domain Name System (DNS) is a paid service provided by 3rd parties and not hosted by our servers.


### id713607870
[[2024-04-30]] 18:40
> Users access websites through domain names, such as api.mysite.com. Usually, the Domain Name System (DNS) is a paid service provided by 3rd parties and not hosted by our servers.


### id713607877
[[2024-04-30]] 18:40
> Internet Protocol (IP) address is returned to the browser or mobile app. In the example, IP address 15.125.23.214 is returned.


### id713607886
[[2024-04-30]] 18:40
> Once the IP address is obtained, Hypertext Transfer Protocol (HTTP) [1] requests are sent directly to your web server.


### id713607860
[[2024-04-30]] 18:40
> The web server returns HTML pages or JSON response for rendering.


### id713607943
[[2024-04-30]] 18:41
> let us examine the traffic source.


### id713607909
[[2024-04-30]] 18:40
> Web application: it uses a combination of server-side languages (Java, Python, etc.) to handle business logic, storage, etc., and client-side languages (HTML and JavaScript) for presentation.


### id713607973
[[2024-04-30]] 18:41
> Mobile application: HTTP protocol is the communication protocol between the mobile app and the web server. JavaScript Object Notation (JSON) is commonly used API response format to transfer data due to its simplicity. An example of the API response in JSON format


### id713608093
[[2024-04-30]] 18:42
> With the growth of the user base, one server is not enough, and we need multiple servers: one for web/mobile traffic, the other for the database (Figure 3). Separating web/mobile traffic (web tier) and database (data tier) servers allows them to be scaled independently.


### id713608118
[[2024-04-30]] 18:43
> Relational databases are also called a relational database management system (RDBMS) or SQL database. The most popular ones are MySQL, Oracle database, PostgreSQL, etc. Relational databases represent and store data in tables and rows. You can perform join operations using SQL across different database tables.


### id713608132
[[2024-04-30]] 18:43
> Non-Relational databases are also called NoSQL databases. Popular ones are CouchDB, Neo4j, Cassandra, HBase, Amazon DynamoDB, etc. [2]. These databases are grouped into four categories: key-value stores, graph stores, column stores, and document stores. Join operations are generally not supported in non-relational databases.


### id713614009
[[2024-04-30]] 19:08
> Let us take a look at the design:
> • A user gets the IP address of the load balancer from DNS.
> • A user connects the load balancer with this IP address.
> • The HTTP request is routed to either Server 1 or Server 2.
> • A web server reads user data from a slave database.
> • A web server routes any data-modifying operations to the master database. This includes write, update, and delete operations.


### id713608903
[[2024-04-30]] 18:44
> Non-relational databases might be the right choice if:
> • Your application requires super-low latency.
> • Your data are unstructured, or you do not have any relational data.
> • You only need to serialize and deserialize data (JSON, XML, YAML, etc.).
> • You need to store a massive amount of data.


### id713613999
[[2024-04-30]] 19:08
> A cache is a temporary storage area that stores the result of expensive responses or frequently accessed data in memory so that subsequent requests are served more quickly.


### id713609227
[[2024-04-30]] 18:45
> Vertical scaling, referred to as “scale up”, means the process of adding more power (CPU, RAM, etc.) to your servers. Horizontal scaling, referred to as “scale-out”, allows you to scale by adding more servers into your pool of resources.


### id713609336
[[2024-04-30]] 18:45
> Vertical scaling has a hard limit. It is impossible to add unlimited CPU and memory to a single server.


### id713609339
[[2024-04-30]] 18:45
> • Vertical scaling does not have failover and redundancy. If one server goes down, the website/app goes down with it completely.


### id713613834
[[2024-04-30]] 19:07
> After receiving a request, a web server first checks if the cache has the available response. If it has, it sends data back to the client. If not, it queries the database, stores the response in cache, and sends it back to the client. This caching strategy is called a read-through cache.


### id713609613
[[2024-04-30]] 18:46
> users are connected to the web server directly. Users will unable to access the website if the web server is offline. In another scenario, if many users access the web server simultaneously and it reaches the web server’s load limit, users generally experience slower response or fail to connect to the server.


### id713609772
[[2024-04-30]] 18:47
> A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set.


### id713613825
[[2024-04-30]] 19:07
> Considerations for using cache
> Here are a few considerations for using a cache system:


### id713613810
[[2024-04-30]] 19:07
> Decide when to use cache. Consider using cache when data is read frequently but modified infrequently. Since cached data is stored in volatile memory, a cache server is not ideal for persisting data. For instance, if a cache server restarts, all the data in memory is lost. Thus, important data should be saved in persistent data stores.


### id713609862
[[2024-04-30]] 18:47
> A private IP is an IP address reachable only between servers in the same network; however, it is unreachable over the internet.


### id713609864
[[2024-04-30]] 18:47
> The load balancer communicates with web servers through private IPs.


### id713609902
[[2024-04-30]] 18:48
> oad balancer and a second web server are added, we successfully solved no failover issue and improved the availability of the web tier

- [n] load balancer solves the problem of no failover issue and improves availability  * [View Highlight](https://read.readwise.io/read/01hwrpgpnx9v6d8mtbyxbhp93d)


### id713610227
[[2024-04-30]] 18:49
> If server 1 goes offline, all the traffic will be routed to server 2. This prevents the website from going offline. We will also add a new healthy web server to the server pool to balance the load.


### id713610229
[[2024-04-30]] 18:49
> If the website traffic grows rapidly, and two servers are not enough to handle the traffic, the load balancer can handle this problem gracefully. You only need to add more servers to the web server pool, and the load balancer automatically starts to send requests to them.


### id713610311
[[2024-04-30]] 18:50
> Database replication can be used in many database management systems, usually with a master/slave relationship between the original (master) and the copies (slaves)


### id713610330
[[2024-04-30]] 18:50
> A master database generally only supports write operations. A slave database gets copies of the data from the master database and only supports read operations. All the data-modifying commands like insert, delete, or update must be sent to the master database.


### id713610327
[[2024-04-30]] 18:50
> Most applications require a much higher ratio of reads to writes; thus, the number of slave databases in a system is usually larger than the number of master databases.


### id713611278
[[2024-04-30]] 18:52
> Advantages of database replication:


### id713611272
[[2024-04-30]] 18:52
> Better performance: In the master-slave model, all writes and updates happen in master nodes; whereas, read operations are distributed across slave nodes. This model improves performance because it allows more queries to be processed in parallel.


### id713611281
[[2024-04-30]] 18:52
> Reliability: If one of your database servers is destroyed by a natural disaster, such as a typhoon or an earthquake, data is still preserved. You do not need to worry about data loss because data is replicated across multiple locations.


### id713611283
[[2024-04-30]] 18:53
> High availability: By replicating data across different locations, your website remains in operation even if a database is offline as you can access data stored in another database server.


### id713611321
[[2024-04-30]] 18:53
> We ask the same question here: what if one of the databases goes offline?


### id713611299
[[2024-04-30]] 18:53
> If only one slave database is available and it goes offline, read operations will be directed to the master database temporarily. As soon as the issue is found, a new slave database will replace the old one. In case multiple slave databases are available, read operations are redirected to other healthy slave databases. A new database server will replace the old one.


### id713611435
[[2024-04-30]] 18:54
> If the master database goes offline, a slave database will be promoted to be the new master. All the database operations will be temporarily executed on the new master database. A new slave database will replace the old one for data replication immediately. In production systems, promoting a new master is more complicated as the data in a slave database might not be up to date. The missing data needs to be updated by running data recovery scripts. Although some other replication methods like multi-masters and circular replication could help, those setups are more complicated; and their discussions are beyond the scope of this course. Interested readers should refer to the listed reference materials


### id713613144
[[2024-04-30]] 19:02
> Let us take a look at the design:
> • A user gets the IP address of the load balancer from DNS.
> • A user connects the load balancer with this IP address.
> • The HTTP request is routed to either Server 1 or Server 2.
> • A web server reads user data from a slave database.
> • A web server routes any data-modifying operations to the master database. This includes write, update, and delete operations.


### id713613542
[[2024-04-30]] 19:02
> A cache is a temporary storage area that stores the result of expensive responses or frequently accessed data in memory so that subsequent requests are served more quickly.


### id713613691
[[2024-04-30]] 19:05
> The cache tier is a temporary data store layer, much faster than the database. The benefits of having a separate cache tier include better system performance, ability to reduce database workloads, and the ability to scale the cache tier independently.


### id713616609
[[2024-04-30]] 19:24
> Eviction Policy: Once the cache is full, any requests to add items to the cache might cause existing items to be removed. This is called cache eviction. Least-recently-used (LRU) is the most popular cache eviction policy. Other eviction policies, such as the Least Frequently Used (LFU) or First in First Out (FIFO), can be adopted to satisfy different use cases.


### id713616880
[[2024-04-30]] 19:25
> A CDN is a network of geographically dispersed servers used to deliver static content. CDN servers cache static content like images, videos, CSS, JavaScript files, etc.


### id713614807
[[2024-04-30]] 19:16
> Expiration policy. It is a good practice to implement an expiration policy. Once cached data is expired, it is removed from the cache. When there is no expiration policy, cached data will be stored in the memory permanently. It is advisable not to make the expiration date too short as this will cause the system to reload data from the database too frequently. Meanwhile, it is advisable not to make the expiration date too long as the data can become stale.


### id713614873
[[2024-04-30]] 19:17
> Consistency: This involves keeping the data store and the cache in sync. Inconsistency can happen because data-modifying operations on the data store and cache are not in a single transaction. When scaling across multiple regions, maintaining consistency between the data store and cache is challenging. For further details, refer to the paper titled “Scaling Memcache at Facebook” published by Facebook [7].


### id713614866
[[2024-04-30]] 19:17
> Mitigating failures: A single cache server represents a potential single point of failure (SPOF), defined in Wikipedia as follows: “A single point of failure (SPOF) is a part of a system that, if it fails, will stop the entire system from working” [8]. As a result, multiple cache servers across different data centers are recommended to avoid SPOF. Another recommended approach is to overprovision the required memory by certain percentages. This provides a buffer as the memory usage increases.


### id713617020
[[2024-04-30]] 19:27
> Cost: CDNs are run by third-party providers, and you are charged for data transfers in and out of the CDN. Caching infrequently used assets provides no significant benefits so you should consider moving them out of the CDN.

- [n] infrequently used items: don’t cache. Wastage of cache memory.  * [View Highlight](https://read.readwise.io/read/01hwrrr6dewcj0yrt4gyenp0kh)


### id713617107
[[2024-04-30]] 19:28
> Setting an appropriate cache expiry: For time-sensitive content, setting a cache expiry time is important. The cache expiry time should neither be too long nor too short. If it is too long, the content might no longer be fresh. If it is too short, it can cause repeat reloading of content from origin servers to the CDN.


### id713617141
[[2024-04-30]] 19:28
> CDN fallback: You should consider how your website/application copes with CDN failure. If there is a temporary CDN outage, clients should be able to detect the problem and request resources from the origin.


### id713617143
[[2024-04-30]] 19:28
> Invalidating files: You can remove a file from the CDN before it expires by performing one of the following operations:


### id713617150
[[2024-04-30]] 19:28
> Invalidate the CDN object using APIs provided by CDN vendors.


### id713617155
[[2024-04-30]] 19:28
> • Use object versioning to serve a different version of the object. To version an object, you can add a parameter to the URL, such as a version number. For example, version number 2 is added to the query string: image.png?v=2.


### id713620649
[[2024-04-30]] 19:30
> Static assets (JS, CSS, images, etc.,) are no longer served by web servers. They are fetched from the CDN for better performance.


### id713620658
[[2024-04-30]] 19:30
> The database load is lightened by caching data.


## New highlights added April 30, 2024 at 10:43 PM
### id713627692
[[2024-04-30]] 19:40
> Dynamic content caching is a relatively new concept and beyond the scope of this course. It enables the caching of HTML pages that are based on request path, query strings, cookies, and request headers. Refer to the article mentioned in reference material [9] for more about this. This course focuses on how to use CDN to cache static content.


### id713627050
[[2024-04-30]] 19:32
> Now it is time to consider scaling the web tier horizontally. For this, we need to move state (for instance user session data) out of the web tier. A good practice is to store session data in the persistent storage such as relational database or NoSQL. Each web server in the cluster can access state data from databases. This is called stateless web tier.


### id713627154
[[2024-04-30]] 19:34
> The issue is that every request from the same client must be routed to the same server. This can be done with sticky sessions in most load balancers [10]; however, this adds the overhead. Adding or removing servers is much more difficult with this approach. It is also challenging to handle server failures.

- [n] How do you handle failover for servers with sticky sessions?  * [View Highlight](https://read.readwise.io/read/01hwrs58cshpzf6d43qc7yx72b)


### id713627304
[[2024-04-30]] 19:36
> we move the session data out of the web tier and store them in the persistent data store. The shared data store could be a relational database, Memcached/Redis, NoSQL, etc. The


### id713627302
[[2024-04-30]] 19:36
> NoSQL data store is chosen as it is easy to scale. Autoscaling means adding or removing web servers automatically based on the traffic load. After the state data is removed out of web servers, auto-scaling of the web tier is easily achieved by adding or removing servers based on traffic load.


### id713627376
[[2024-04-30]] 19:37
> In normal operation, users are geoDNS-routed, also known as geo-routed, to the closest data center, with a split traffic of *x%* in US-East and *(100 – x)%* in US-West.


### id713627367
[[2024-04-30]] 19:37
> geoDNS is a DNS service that allows domain names to be resolved to IP addresses based on the location of a user.


### id713627379
[[2024-04-30]] 19:37
> In the event of any significant data center outage, we direct all traffic to a healthy data center.


### id713627377
[[2024-04-30]] 19:37
> data center 2 (US-West) is offline, and 100% of the traffic is routed to data center 1 (US-East).


### id713627683
[[2024-04-30]] 19:40
> Traffic redirection: Effective tools are needed to direct traffic to the correct data center. GeoDNS can be used to direct traffic to the nearest data center depending on where a user is located.


### id713627685
[[2024-04-30]] 19:40
> Data synchronization: Users from different regions could use different local databases or caches. In failover cases, traffic might be routed to a data center where data is unavailable. A common strategy is to replicate data across multiple data centers. A previous study shows how Netflix implements asynchronous multi-data center replication


### id713631699
[[2024-04-30]] 19:46
> Test and deployment: With multi-data center setup, it is important to test your website/application at different locations. Automated deployment tools are vital to keep services consistent through all the data centers


### id713631755
[[2024-04-30]] 19:46
> A message queue is a durable component, stored in memory, that supports asynchronous communication


### id713631843
[[2024-04-30]] 19:48
> Decoupling makes the message queue a preferred architecture for building a scalable and reliable application.


### id713631915
[[2024-04-30]] 19:48
> With the message queue, the producer can post a message to the queue when the consumer is unavailable to process it. The consumer can read messages from the queue even when the producer is unavailable.


### id713631912
[[2024-04-30]] 19:48
> Consider the following use case: your application supports photo customization, including cropping, sharpening, blurring, etc. Those customization tasks take time to complete. In Figure 18, web servers publish photo processing jobs to the message queue. Photo processing workers pick up jobs from the message queue and asynchronously perform photo customization tasks. The producer and the consumer can be scaled independently. When the size of the queue becomes large, more workers are added to reduce the processing time. However, if the queue is empty most of the time, the number of workers can be reduced.


### id713631937
[[2024-04-30]] 19:49
> Monitoring error logs is important because it helps to identify errors and problems in the system. You can monitor error logs at per server level or use tools to aggregate them to a centralized service for easy search and viewing.


### id713631944
[[2024-04-30]] 19:49
> Collecting different types of metrics help us to gain business insights and understand the health status of the system.


### id713632041
[[2024-04-30]] 19:50
> Host level metrics: CPU, Memory, disk I/O, etc.


### id713632047
[[2024-04-30]] 19:50
> Aggregated level metrics: for example, the performance of the entire database tier, cache tier, etc.


### id713632056
[[2024-04-30]] 19:50
> Key business metrics: daily active users, retention, revenue, etc.


### id713632099
[[2024-04-30]] 19:51
> When a system gets big and complex, we need to build or leverage automation tools to improve productivity.


### id713632203
[[2024-04-30]] 19:53
> Continuous integration is a good practice, in which each code check-in is verified through automation, allowing teams to detect problems early. Besides, automating your build, test, deploy process, etc.


### id713632274
[[2024-04-30]] 19:53
> The design includes a message queue, which helps to make the system more loosely coupled and failure resilient.


### id713632278
[[2024-04-30]] 19:53
> Logging, monitoring, metrics, and automation tools are included.


### id713632439
[[2024-04-30]] 19:55
> ertical scaling, also known as scaling up, is the scaling by adding more power (CPU, RAM, DISK, etc.) to an existing machine


### id713632487
[[2024-04-30]] 19:56
> • You can add more CPU, RAM, etc. to your database server, but there are hardware limits. If you have a large user base, a single server is not enough.
> • Greater risk of single point of failures.
> • The overall cost of vertical scaling is high. Powerful servers are much more expensive.


### id713632489
[[2024-04-30]] 19:56
> Horizontal scaling, also known as sharding, is the practice of adding more servers.


### id713627793
[[2024-04-30]] 19:41
> R. Nishtala, "Facebook, Scaling Memcache at," 10th USENIX Symposium on Networked Systems Design and Implementation (NSDI ’13).


### id713632495
[[2024-04-30]] 19:56
> Sharding separates large databases into smaller, more easily managed parts called shards. Each shard shares the same schema, though the actual data on each shard is unique to the shard.


### id713632534
[[2024-04-30]] 19:56
> The most important factor to consider when implementing a sharding strategy is the choice of the sharding key. Sharding key (known as a partition key) consists of one or more columns that determine how data is distributed


### id713632539
[[2024-04-30]] 19:56
> When choosing a sharding key, one of the most important criteria is to choose a key that can evenly distributed data.


### id713632554
[[2024-04-30]] 19:56
> **Resharding data**: Resharding data is needed when 1) a single shard could no longer hold more data due to rapid growth. 2) Certain shards might experience shard exhaustion faster than others due to uneven data distribution. When shard exhaustion happens, it requires updating the sharding function and moving data around. Consistent hashing is a commonly used technique to solve this problem.


### id713632569
[[2024-04-30]] 19:57
> **Celebrity problem**: This is also called a hotspot key problem. Excessive access to a specific shard could cause server overload. Imagine data for Katy Perry, Justin Bieber, and Lady Gaga all end up on the same shard. For social applications, that shard will be overwhelmed with read operations. To solve this problem, we may need to allocate a shard for each celebrity. Each shard might even require further partition.


### id713632606
[[2024-04-30]] 19:57
> **Join and de-normalization**: Once a database has been sharded across multiple servers, it is hard to perform join operations across database shards. A common workaround is to de-normalize the database so that queries can be performed in a single table.


