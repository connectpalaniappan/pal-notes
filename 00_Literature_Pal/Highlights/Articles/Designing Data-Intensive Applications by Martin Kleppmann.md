---
title: Designing Data-Intensive Applications
full Title: Designing Data-Intensive Applications
author: Martin Kleppmann
URL: https://readwise.io/reader/document_raw_content/2276328
published date: 2017-03-01
category: articles
source: reader
tags: [author/pal_read,people/pal,shortlist,medium/articles, author/Martin_Kleppmann, reader/reader, date/2024-06-11, area/reader]
created: 2024-06-11
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Martin Kleppmann]]
note:: 
source:: [[reader]]
url:: [articles URL](https://readwise.io/reader/document_raw_content/2276328)
image_url:: [articles image URL](https://kbimages1-a.akamaihd.net/42e841e7-4c04-4b8c-a881-89eef3c85bb1/1200/1200/False/designing-data-intensive-applications.jpg)
category:: [[articles]]
date:: [[2024-06-11]]
last_highlighted_date:: [[2024-06-11]]
published_date:: [[2017-03-01]]
summary:: This article discusses the challenges of building reliable data systems, including failures in software or hardware, interruptions in the network, and race conditions between clients. It covers different isolation levels and techniques for preventing lost updates, and explores how distributed databases handle concurrency control and eventual consistency. The article also highlights the importance of detecting concurrent writes and preventing lost updates in leaderless datastores.


![rw-book-cover](https://kbimages1-a.akamaihd.net/42e841e7-4c04-4b8c-a881-89eef3c85bb1/1200/1200/False/designing-data-intensive-applications.jpg)

## Highlights
### id732282659
[[2024-06-11]] 11:05
> Technology is a powerful force in our society. Data, software, and communication can be used for bad: to entrench unfair power structures, to undermine human rights, and to protect vested interests. But they can also be used for good: to make underrepresented people’s voices heard, to create opportunities for everyone, and to avert disasters. This book is dedicated to everyone working toward the good.

- [n] Create software for good  * [View Highlight](https://read.readwise.io/read/01j040ra394fqb602fz0n5ag2j)


## New highlights added June 11, 2024 at 12:09 PM
### id732286999
[[2024-06-11]] 11:16
> Free and open source software has become very successful and is now preferred to commercial or bespoke in-house software in many environments.


### id732287057
[[2024-06-11]] 11:17
> CPU clock speeds are barely increasing, but multi-core processors are standard, and networks are getting faster. This means parallelism is only going to increase.


## New highlights added June 12, 2024 at 8:50 AM
### id732761250
[[2024-06-12]] 08:10
> We call an application data-intensive if data is its primary challenge—the quantity of data, the complexity of data, or the speed at Preface | xiii


### id732761254
[[2024-06-12]] 08:10
> which it is changing—as opposed to compute-intensive, where CPU cycles are the bottleneck


### id732767810
[[2024-06-12]] 08:41
> there are enduring principles that remain true, no matter which version of a particular tool you are using. If you understand those principles, you’re in a position to see where each tool fits in, how to make good use of it, and how to avoid its pitfalls.


### id732769446
[[2024-06-12]] 08:46
> dig into the internals of those systems, tease apart their key algorithms, dis‐ cuss their principles and the trade-offs they have to make.


## New highlights added June 12, 2024 at 9:50 AM
### id732775368
[[2024-06-12]] 09:17
> Many applications today are data-intensive, as opposed to compute-intensive. Raw CPU power is rarely a limiting factor for these applications—bigger problems are usually the amount of data, the complexity of data, and the speed at which it is changing.

- [n] Data intensive applications 
   - Amount of data 
   - Complexity of data 
   - Speed at which it changes  * [View Highlight](https://read.readwise.io/read/01j06cxvww7rtm045ekg8w0jvb)


## New highlights added June 12, 2024 at 11:49 AM
### id732802855
[[2024-06-12]] 10:55
> For example, there are datastores that are also used as mes‐ sage queues (Redis), and there are message queues with database-like durability guar‐ antees (Apache Kafka).


### id732802920
[[2024-06-12]] 10:56
> For example, if you have an application-managed caching layer (using Memcached or similar), or a full-text search server (such as Elasticsearch or Solr) separate from your main database, it is normally the application code’s responsibility to keep those caches and indexes in sync with the main database.


### id732803148
[[2024-06-12]] 10:58
> Your composite data system may provide certain guarantees: e.g., that the cache will be correctly invalidated or upda‐ ted on writes so that outside clients see consistent results.


### id732803173
[[2024-06-12]] 10:59
> How do you ensure that the data remains correct and complete, even when things go wrong internally?

- [n] data integrity  * [View Highlight](https://read.readwise.io/read/01j06js1kb687cx88ae8ghjq2f)


### id732803305
[[2024-06-12]] 10:59
> How do you scale to handle an increase in load?

- [n] Scalability  * [View Highlight](https://read.readwise.io/read/01j06jtmvscmrcbwyq8y3sfxr1)


### id732803314
[[2024-06-12]] 11:00
> How do you provide consistently good performance to clients, even when parts of your system are degraded?

- [n] fault tolerance  * [View Highlight](https://read.readwise.io/read/01j06jtxtzfvchxrb3g2ssdkwj)


### id732803339
[[2024-06-12]] 11:00
> Reliability The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardware or soft‐ ware faults, and even human error).


### id732803371
[[2024-06-12]] 11:00
> Scalability As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth.


### id732803376
[[2024-06-12]] 11:00
> Maintainability Over time, many different people will work on the system (engineering and oper‐ ations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively.


### id732810657
[[2024-06-12]] 11:26
> Everybody has an intuitive idea of what it means for something to be reliable or unre‐ liable. For software, typical expectations include:

- [n] performs on valid load, avoid load due to unauthorized access, handle user failure elegantly  * [View Highlight](https://read.readwise.io/read/01j06mahyngf0taa3sy7x5b0sq)


### id732810650
[[2024-06-12]] 11:25
> The application performs the function that the user expected. • It can tolerate the user making mistakes or using the software in unexpected ways.
> • Its performance is good enough for the required use case, under the expected load and data volume.
> • The system prevents any unauthorized access and abuse.


### id732811022
[[2024-06-12]] 11:27
> The things that can go wrong are called faults, and systems that anticipate faults and can cope with them are called fault-tolerant or resilient.


### id732811093
[[2024-06-12]] 11:31
> A fault is usually defined as one com‐ ponent of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user.

- [n] Recently when there was a fault in memcache failure, the entire monolith stopped working which is a failure.  * [View Highlight](https://read.readwise.io/read/01j06mej5f6021wnzxe7x8ewqe)


### id732812437
[[2024-06-12]] 11:37
> Our first response is usually to add redundancy to the individual hardware compo‐ nents in order to reduce the failure rate of the system.

- [n] Redundancy is a good strategy to build fault tolerance for disk failures  * [View Highlight](https://read.readwise.io/read/01j06mv9fatejt7a1gx7yby8r1)


### id732812967
[[2024-06-12]] 11:39
> Disks may be set up in a RAID configuration, servers may have dual power supplies and hot-swappable CPUs, and datacenters may have batteries and diesel generators for backup power.


### id732813766
[[2024-06-12]] 11:42
> systems also have operational advantages: a single-server system requires planned downtime if you need to reboot the machine


### id732813750
[[2024-06-12]] 11:42
> a system that can tolerate machine failure can be patched one node at a time, without downtime of the entire system (a rolling upgrade;


### id732814359
[[2024-06-12]] 11:46
> A software bug that causes every instance of an application server to crash when given a particular bad input.

- [n] Our monolith was going down due to recursive calls being made to pull the parent-child records from the database when the child’s parent is also the parent’s child  * [View Highlight](https://read.readwise.io/read/01j06nehzyqrgbnfnbgvsq9wa7)


## New highlights added June 12, 2024 at 12:49 PM
### id732827617
[[2024-06-12]] 12:35
> A service that the system depends on that slows down, becomes unresponsive, or starts returning corrupted responses.
> • Cascading failures, where a small fault in one component triggers a fault in another component, which in turn triggers further faults [10]


### id732827372
[[2024-06-12]] 12:35
> Design systems in a way that minimizes opportunities for error. For example, well-designed abstractions, APIs, and admin interfaces make it easy to do “the right thing” and discourage “the wrong thing.” However, if the interfaces are too restrictive people will work around them, negating their benefit, so this is a tricky balance to get right.


### id732827371
[[2024-06-12]] 12:35
> Decouple the places where people make the most mistakes from the places where they can cause failures. In particular, provide fully featured non-production sandbox environments where people can explore and experiment safely, using real data, without affecting real users.


### id732827676
[[2024-06-12]] 12:36
> Test thoroughly at all levels, from unit tests to whole-system integration tests and manual tests [3]. Automated testing is widely used, well understood, and espe‐ cially valuable for covering corner cases that rarely arise in normal operation.

- [n] Comprehensive testing  * [View Highlight](https://read.readwise.io/read/01j06rabfwbqzdgwjjqy1dpnyn)


### id732827702
[[2024-06-12]] 12:36
> Allow quick and easy recovery from human errors, to minimize the impact in the case of a failure. For example, make it fast to roll back configuration changes, roll out new code gradually (so that any unexpected bugs affect only a small subset of users), and provide tools to recompute data (in case it turns out that the old com‐ putation was incorrect).

- [n] Faster rollbacks  * [View Highlight](https://read.readwise.io/read/01j06raqgd9ce2xqw3x19w1f6n)


### id732828194
[[2024-06-12]] 12:37
> Set up detailed and clear monitoring, such as performance metrics and error rates. In other engineering disciplines this is referred to as telemetry. (Once a rocket has left the ground, telemetry is essential for tracking what is happening, and for understanding failures [14].) Monitoring can show us early warning sig‐ nals and allow us to check whether any assumptions or constraints are being vio‐ lated. When a problem occurs, metrics can be invaluable in diagnosing the issue.

- [n] Observability  * [View Highlight](https://read.readwise.io/read/01j06rd00mkqgg1f3wc622app0)


### id732831433
[[2024-06-12]] 12:44
> First, we need to succinctly describe the current load on the system; only then can we discuss growth questions (what happens if our load doubles?). Load can be described with a few numbers which we call load parameters.


### id732831619
[[2024-06-12]] 12:45
> best choice of parameters depends on the architecture of your system: it may be requests per second to a web server, the ratio of reads to writes in a database, the number of simultaneously active users in a chat room, the hit rate on a cache, or something else.

- [n] Load parameters 
   - Request per second to a web server 
   - Ratio of reads to writes in a database 
   - Simultaneously active users in a chat room 
   - Hit rate on a cache  * [View Highlight](https://read.readwise.io/read/01j06rtaevd79tn26bpn2t20az)


### id732831876
[[2024-06-12]] 12:46
> Twitter’s scaling challenge is not primarily due to tweet volume,
> but due to fan-outii
> —each user follows many people, and each user is followed by
> many people.


## New highlights added June 12, 2024 at 1:49 PM
### id732837285
[[2024-06-12]] 13:10
> Maintain a cache for each user’s home timeline—like a mailbox of tweets for each recipient user (see Figure 1-3). When a user posts a tweet, look up all the people who follow that user, and insert the new tweet into each of their home timeline caches. The request to read the home timeline is then cheap, because its result has been computed ahead of time.

- [n] Cache will be useful for read requests
   Preprocessing also saves a ton of time  * [View Highlight](https://read.readwise.io/read/01j06t8m1b5dc3fjdy6k2d5kwh)


### id732839321
[[2024-06-12]] 13:14
> Most users’ tweets continue to be fanned out to home timelines at the time when they are posted, but a small number of users with a very large number of followers (i.e., celebrities) are excepted from this fan-out. Tweets from any celebrities that a user may follow are fetched separately and merged with that user’s home timeline when it is read, like in approach 1.

- [n] Hybrid approach 
   - database when the fan-out is high. Makes it low cost to avoid writing multiple cache therby increasing write times. 
   - cache when the fan-out is low. Makes it low cost during writes as we update a minimal number of row entries.  * [View Highlight](https://read.readwise.io/read/01j06tdf0s0ma1wmkfetjvrgge)


## New highlights added June 13, 2024 at 10:59 AM
### id733317402
[[2024-06-13]] 09:51
> When you increase a load parameter and keep the system resources (CPU, mem‐ ory, network bandwidth, etc.) unchanged, how is the performance of your system affected?


### id733317403
[[2024-06-13]] 09:51
> When you increase a load parameter, how much do you need to increase the resources if you want to keep performance unchanged?


### id733318229
[[2024-06-13]] 09:53
> In a batch processing system such as Hadoop, we usually care about throughput—the
> number of records we can process per second, or the total time it takes to run a job
> on a dataset of a certain size.iii
> In online systems, what’s usually more important is the
> service’s response time—that is, the time between a client sending a request and
> receiving a response.


### id733318154
[[2024-06-13]] 09:53
> Latency and response time are often used synonymously, but they are not the same. The response time is what the client sees: besides the actual time to process the request (the service time), it includes network delays and queueing delays. Latency is the duration that a request is waiting to be handled—during which it is latent, await‐ ing service

- [n] Nice difference between latency and response time  * [View Highlight](https://read.readwise.io/read/01j091d729t6ab47p9at6kfcmj)


### id733318499
[[2024-06-13]] 09:54
> Usually it is better to use percentiles.


### id733318998
[[2024-06-13]] 09:56
> t’s important to keep those customers happy by ensuring the website is fast for them: Amazon has also observed that a 100 ms increase in response time reduces sales by 1% [20], and others report that a 1-second slowdown reduces a customer sat‐ isfaction metric by 16% [21, 22].


### id733319076
[[2024-06-13]] 09:57
> percentiles are often used in service level objectives (SLOs) and service level agreements (SL


### id733319073
[[2024-06-13]] 09:57
> SLAs), contracts that define the expected performance and availa‐ bility of a service. An SLA may state that the service is considered to be up if it has a median response time of less than 200 ms and a 99th percentile under 1 s (if the response time is longer, it might as well be down), and the service may be required to be up at least 99.9% of the time.


### id733319159
[[2024-06-13]] 09:58
> Queueing delays often account for a large part of the response time at high percen‐ tiles. As a server can only process a small number of things in parallel (limited, for


### id733319172
[[2024-06-13]] 09:58
> example, by its number of CPU cores), it only takes a small number of slow requests to hold up the processing of subsequent requests—an effect sometimes known as head-of-line blocking.


## New highlights added June 13, 2024 at 12:59 PM
### id733379543
[[2024-06-13]] 12:23
> Even if only a small percentage of backend calls are slow, the chance of getting a slow call increases if an end-user request requires multiple back‐ end calls, and so a higher proportion of end-user requests end up being slow (an effect known as tail latency amplification


## New highlights added June 13, 2024 at 3:02 PM
### id733401186
[[2024-06-13]] 14:16
> The naïve implementation is to keep a list of response times for all requests within the time window and to sort that list every minute.


### id733403734
[[2024-06-13]] 14:26
> calculate a good approximation of percentiles at minimal CPU and memory cost, such as forward decay [25], t-digest [26], or HdrHistogram

- [n] Good percentile calculation algorithm: decay, t-digest or HdrHistogram  * [View Highlight](https://read.readwise.io/read/01j09grgx3vkg1vghde0rw7f35)


### id733405263
[[2024-06-13]] 14:27
> scaling up (vertical scaling, moving to a more powerful machine) and scaling out (horizontal scaling, distributing the load across multiple smaller machines).


### id733407299
[[2024-06-13]] 14:29
> Distributing load across multiple machines is also known as a shared-nothing architecture.


### id733407759
[[2024-06-13]] 14:30
> Some systems are elastic, meaning that they can automatically add computing resour‐ ces when they detect a load increase, whereas other systems are scaled manually (a human analyzes the capacity and decides to add more machines to the system)


## New highlights added June 13, 2024 at 5:21 PM
### id733432236
[[2024-06-13]] 16:40
> distributing stateless services across multiple machines is fairly straightfor‐ ward, taking stateful data systems from a single node to a distributed setup can intro‐ duce a lot of additional complexity.


### id733436106
[[2024-06-13]] 16:53
> The architecture of systems that operate at large scale is usually highly specific to the application—there is no such thing as a generic, one-size-fits-all scalable architecture (informally known as magic scaling sauce)


### id733436112
[[2024-06-13]] 16:54
> problem may be the volume of reads, the volume of writes, the volume of data to store, the complexity of the data, the response time requirements, the access patterns, or (usually) some mixture of all of these plus many more issues.


## New highlights added June 13, 2024 at 11:02 PM
### id733493782
[[2024-06-13]] 21:08
> majority of the cost of software is not in its initial development, but in its ongoing maintenance—fixing bugs, keeping its systems operational, investigating failures, adapting it to new platforms, modifying it for new use cases, repaying technical debt, and adding new features.
> Yet, unfortunately, many people working on software


## New highlights added June 15, 2024 at 5:28 PM
### id733693321
[[2024-06-14]] 11:59
> majority of the cost of software is not in its initial develop‐ ment, but in its ongoing maintenance—fixing bugs, keeping its systems operational, investigating failures, adapting it to new platforms, modifying it for new use cases, repaying technical debt, and adding new features.


## New highlights added June 16, 2024 at 7:08 PM
### id734638237
[[2024-06-16]] 18:44
> good operations can often work around the limitations of bad (or incomplete) software, but good software cannot run reliably with bad opera‐ tions


## New highlights added June 16, 2024 at 10:51 PM
### id734688709
[[2024-06-16]] 22:10
> A good operations team typically is responsible for the following, and more [29]:


### id734688699
[[2024-06-16]] 22:10
> Monitoring the health of the system and quickly restoring service if it goes into a bad state • Tracking down the cause of problems, such as system failures or degraded per‐ formance • Keeping software and platforms up to date, including security patches • Keeping tabs on how different systems affect each other, so that a problematic change can be avoided before it causes damage


### id734688701
[[2024-06-16]] 22:10
> Anticipating future problems and solving them before they occur (e.g., capacity planning) • Establishing good practices and tools for deployment, configuration manage‐ ment, and more • Performing complex maintenance tasks, such as moving an application from one platform to another • Maintaining the security of the system as configuration changes are made • Defining processes that make operations predictable and help keep the produc‐ tion environment stable • Preserving the organization’s knowledge about the system, even as individual people come and go


### id734688706
[[2024-06-16]] 22:10
> Data systems can do various things to make routine tasks easy, including:


### id734688652
[[2024-06-16]] 22:10
> Providing visibility into the runtime behavior and internals of the system, with good monitoring


### id734688596
[[2024-06-16]] 22:10
> Providing good support for automation and integration with standard tools


### id734688415
[[2024-06-16]] 22:10
> Avoiding dependency on individual machines (allowing machines to be taken down for maintenance while the system as a whole continues running uninter‐ rupted)


### id734688399
[[2024-06-16]] 22:10
> Providing good documentation and an easy-to-understand operational model (“If I do X, Y will happen”)


### id734688373
[[2024-06-16]] 22:10
> Providing good default behavior, but also giving administrators the freedom to override defaults when needed


### id734688185
[[2024-06-16]] 22:10
> Self-healing where appropriate, but also giving administrators manual control over the system state when needed


### id734688261
[[2024-06-16]] 22:10
> Exhibiting predictable behavior, minimizing surprises


### id734689503
[[2024-06-16]] 22:14
> A software project mired in complexity is sometimes described as a big ball of mud


### id734689684
[[2024-06-16]] 22:15
> There are various possible symptoms of complexity: e


### id734689682
[[2024-06-16]] 22:15
> explosion of the state space, tight coupling of modules, tangled dependencies, inconsistent naming and terminology, hacks aimed at solving performance problems, special-casing to work around issues elsewhere, and many more.


### id734689734
[[2024-06-16]] 22:16
> In complex software, there is also a greater risk of introducing bugs when mak‐ ing a change: when the system is harder for developers to understand and reason about, hidden assumptions, unintended consequences, and unexpected interactions are more easily overlooked.


### id734690770
[[2024-06-16]] 22:29
> Moseley and Marks [32] define complex‐ ity as accidental if it is not inherent in the problem that the software solves (as seen by the users) but arises only from the implementation.

- [n] Whatte a definition of complexity! Complexity in implementation is so bad. Complexity in user requirements should be fine.  * [View Highlight](https://read.readwise.io/read/01j0j3tjrfg5w5bvp82dk2nvqb)


### id734690874
[[2024-06-16]] 22:29
> One of the best tools we have for removing accidental complexity is abstraction. A good abstraction can hide a great deal of implementation detail behind a clean, simple-to-understand façade. A good abstraction can also be used for a wide range of different applications. Not only is this reuse more efficient than reimplementing a similar thing multiple times, but it also leads to higher-quality software, as quality improvements in the abstracted component benefit all applications that use it.


### id734692797
[[2024-06-16]] 22:38
> high-level programming languages are abstractions that hide machine code, CPU registers, and syscalls. SQL is an abstraction that hides complex on-disk and in-memory data structures, concurrent requests from other clients, and inconsis‐ tencies after crashes.


### id734692840
[[2024-06-16]] 22:38
> Of course, when programming in a high-level language, we are still using machine code; we are just not using it directly, because the programming language abstraction saves us from having to think about it.


### id734695101
[[2024-06-16]] 22:49
> In terms of organizational processes, Agile working patterns provide a framework for adapting to change. The Agile community has also developed technical tools and pat‐ terns that are helpful when developing software in a frequently changing environ‐ ment, such as test-driven development (TDD) and refactoring.

- [n] How agile development could help with ever changing software?  * [View Highlight](https://read.readwise.io/read/01j0j507q52dzhfn5yew4zcp5z)


### id734695266
[[2024-06-16]] 22:49
> The ease with which you can modify a data system, and adapt it to changing require‐ ments, is closely linked to its simplicity and its abstractions: simple and easy-to- understand systems are usually easier to modify than complex ones. But since this is such an important idea, we will use a different word to refer to agility on a data sys‐ tem level: evolvability [34].


### id734695506
[[2024-06-16]] 22:50
> security, reliability, compliance, scalability, compatibil‐ ity, and maintainability


## New highlights added June 17, 2024 at 5:27 PM
### id735003241
[[2024-06-17]] 16:30
> As an application developer, you look at the real world (in which there are peo‐ ple, organizations, goods, actions, money flows, sensors, etc.) and model it in terms of objects or data structures, and APIs that manipulate those data struc‐ tures. Those structures are often specific to your application.
> 2. When you want to store those data structures, you express them in terms of a general-purpose data model, such as JSON or XML documents, tables in a rela‐ tional database, or a graph model.
> 3. The engineers who built your database software decided on a way of representing that JSON/XML/relational/graph data in terms of bytes in memory, on disk, or on a network. The representation may allow the data to be queried, searched, manipulated, and processed in various ways.
> 4. On yet lower levels, hardware engineers have figured out how to represent bytes in terms of electrical currents, pulses of light, magnetic fields, and more.


## New highlights added June 17, 2024 at 10:27 PM
### id735105109
[[2024-06-17]] 22:10
> relational database management systems (RDBMSes) and SQL had become the tools of choice for most people who needed to store and query data with some kind of reg‐ ular structure.


### id735105135
[[2024-06-17]] 22:11
> use cases appear mundane from today’s perspective: typically transaction processing (entering sales or banking trans‐ actions, airline reservations, stock-keeping in warehouses) and batch processing (cus‐ tomer invoicing, payroll, reporting).


### id735105294
[[2024-06-17]] 22:11
> the network model and the hierarchical model


### id735105292
[[2024-06-17]] 22:11
> were the main alternatives, but the relational model came to dominate them.


### id735105360
[[2024-06-17]] 22:13
> The name “NoSQL” is unfortunate, since it doesn’t actually refer to any particular technology—it was originally intended simply as a catchy Twitter hashtag for a meetup on open source, distributed, nonrelational databases in 2009 [


### id735105591
[[2024-06-17]] 22:16
> There are several driving forces behind the adoption of NoSQL databases, including:


### id735105579
[[2024-06-17]] 22:16
> A need for greater scalability than relational databases can easily achieve, includ‐ ing very large datasets or very high write throughput • A widespread preference for free and open source software over commercial database products


### id735105784
[[2024-06-17]] 22:16
> Specialized query operations that are not well supported by the relational model • Frustration with the restrictiveness of relational schemas, and a desire for a more dynamic and expressive data model [5]


### id735105798
[[2024-06-17]] 22:16
> It therefore seems likely that in the foreseeable future, relational databases will continue to be used alongside a broad variety of nonrelational datastores—an idea that is sometimes called polyglot persistence


## New highlights added June 18, 2024 at 9:47 AM
### id735256351
[[2024-06-18]] 08:52
> f data is stored in relational tables, an awkward translation layer is required between the objects in the


### id735256349
[[2024-06-18]] 08:52
> application code and the database model of tables, rows, and columns. The discon‐ nect between the models is sometimes called an impedance mismatch.i


### id735257486
[[2024-06-18]] 08:58
> the most common normalized representation is to put positions, education, and contact information in separate tables, with a foreign key reference to the users table,


### id735257463
[[2024-06-18]] 08:58
> multi-valued data to be stored within a single row, with support for querying and indexing inside those documents. T


### id735257473
[[2024-06-18]] 08:58
> third option is to encode jobs, education, and contact info as a JSON or XML document, store it on a text column in the database, and let the application inter‐ pret its structure and content. In this setup, you typically cannot use the database to query for values inside that encoded column.


### id735257839
[[2024-06-18]] 09:00
> For a data structure like a résumé, which is mostly a self-contained document, a JSON representation can be quite appropriate


### id735258137
[[2024-06-18]] 09:00
> Document-oriented databases like MongoDB [9], RethinkDB [10], CouchDB [11], and Espresso [12] support this data model.


### id735270398
[[2024-06-18]] 09:04
> Some developers feel that the JSON model reduces the impedance mismatch between the application code and the storage layer.


## New highlights added June 18, 2024 at 10:47 AM
### id735290306
[[2024-06-18]] 10:25
> data encoding format.

- [n] Data encoding is the process of converting data from one form to another so that it can be processed efficiently by different systems and applications.  * [View Highlight](https://read.readwise.io/read/01j0nz81y05ye604xjm7rebewa)


## New highlights added June 19, 2024 at 12:42 PM
### id735756172
[[2024-06-19]] 11:58
> The lack of a schema is often cited as an advantage


### id735756614
[[2024-06-19]] 12:00
> there are advantages to having standardized lists of geographic regions and industries, and letting users choose from a drop-down list or autocompleter: • Consistent style and spelling across profiles • Avoiding ambiguity (e.g., if there are several cities with the same name) • Ease of updating—the name is stored in only one place, so it is easy to update across the board if it ever needs to be changed (e.g., change of a city name due to political events) • Localization support—when the site is translated into other languages, the stand‐ ardized lists can be localized, so the region and industry can be displayed in the viewer’s language • Better search—e.g., a search for philanthropists in the state of Washington can match this profile, because the list of regions can encode the fact that Seattle is in Washington (which is not apparent from the string "Greater Seattle Area")


### id735761302
[[2024-06-19]] 12:23
> When you store the text directly, you are duplicating the human-meaningful information in every record that uses it.


### id735761435
[[2024-06-19]] 12:24
> incurs write overheads, and risks inconsistencies (where some copies of the information are updated but others aren’t)


### id735761400
[[2024-06-19]] 12:24
> Removing such duplication is the key idea behind normalization in databases.i


### id735763090
[[2024-06-19]] 12:36
> . In relational databases, it’s normal to refer to rows in other tables by ID, because joins are easy. In document databases, joins are not needed for one-to-many tree structures, and support for joins is often weak.

- [n] In document databases, joins are often weak. Is that true?  * [View Highlight](https://read.readwise.io/read/01j0rs34c17d1k1t3b548kxfw6)


### id735763675
[[2024-06-19]] 12:37
> If the database itself does not support joins, you have to emulate a join in application code by making multiple queries to the database.


## New highlights added June 19, 2024 at 1:42 PM
### id735768272
[[2024-06-19]] 13:00
> Developers had to decide whether to duplicate (denormalize) data or to manually resolve refer‐ ences from one record to another.


## New highlights added June 19, 2024 at 3:42 PM
### id735814339
[[2024-06-19]] 15:24
> While many-to-many relationships and joins are routinely used in relational data‐ bases, document databases and NoSQL reopened the debate on how best to represent such relationships in a database.


### id735816835
[[2024-06-19]] 15:31
> The CODASYL model was a generalization of the hierarchical model. In the tree structure of the hierarchical model, every record has exactly one parent; in the net‐ work model, a record could have multiple parents. For example, there could be one record for the "Greater Seattle Area" region, and every user who lived in that region could be linked to it. This allowed many-to-one and many-to-many relation‐ ships to be modeled.


### id735817923
[[2024-06-19]] 15:34
> The links between records in the network model were not foreign keys, but more like pointers in a programming language (while still being stored on disk). The only way of accessing a record was to follow a path from a root record along these chains of links. This was called an access path.


### id735817964
[[2024-06-19]] 15:34
> With both the hierarchical and the network model, if you didn’t have a path to the data you wanted, you were in a difficult situa‐ tion. You could change the access paths, but then you had to go through a lot of handwritten database query code and rewrite it to handle the new access paths. It was difficult to make changes to an application’s data model.


### id735818217
[[2024-06-19]] 15:36
> What the relational model did, by contrast, was to lay out all the data in the open: a relation (table) is simply a collection of tuples (rows), and that’s it.


### id735818206
[[2024-06-19]] 15:36
> In a relational database, the query optimizer automatically decides which parts of the query to execute in which order, and which indexes to use.


### id735818310
[[2024-06-19]] 15:37
> If you want to query your data in new ways, you can just declare a new index, and queries will automatically use whichever indexes are most appropriate. You don’t need to change your queries to take advantage of a new index


### id735818389
[[2024-06-19]] 15:38
> a key insight of the relational model was this: you only need to build a query optimizer once, and then all applications that use the database can benefit from it. If you don’t have a query opti‐ mizer, it’s easier to handcode the access paths for a particular query than to write a general-purpose optimizer—but the general-purpose solution wins in the long run.


### id735818910
[[2024-06-19]] 15:41
> Document databases reverted back to the hierarchical model in one aspect: storing nested records (one-to-many relationships, like positions, education, and contact_info in Figure 2-1) within their parent record rather than in a separate table.


### id735819105
[[2024-06-19]] 15:41
> in both cases, the related item is referenced by a unique identifier, which is called a foreign key in the relational model and a document reference in the document model


### id735819246
[[2024-06-19]] 15:41
> That identifier is resolved at read time by using a join or follow-up queries.


### id735819332
[[2024-06-19]] 15:41
> main arguments in favor of the document data model are schema flexibility, bet‐ ter performance due to locality, and that for some applications it is closer to the data structures used by the application.


## New highlights added June 19, 2024 at 4:42 PM
### id735819564
[[2024-06-19]] 15:43
> The relational model counters by providing better support for joins, and many-to-one and many-to-many relationships.


### id735819605
[[2024-06-19]] 15:44
> If the data in your application has a document-like structure (i.e., a tree of one-to- many relationships, where typically the entire tree is loaded at once), then it’s proba‐ 38 | Chapter 2: Data Models and Query Languages


### id735819607
[[2024-06-19]] 15:44
> bly a good idea to use a document model. T


### id735819612
[[2024-06-19]] 15:44
> The relational technique of shredding— splitting a document-like structure into multiple tables (like positions, education, and contact_info in Figure 2-1)—can lead to cumbersome schemas and unnecessa‐ rily complicated application code.


### id735820278
[[2024-06-19]] 15:49
> The poor support for joins in document databases may or may not be a problem, depending on the application. For example, many-to-many relationships may never be needed in an analytics application that uses a document database to record which events occurred at which time


## New highlights added June 19, 2024 at 5:42 PM
### id735831708
[[2024-06-19]] 16:43
> Document databases are sometimes called schemaless, but that’s misleading, as the code that reads the data usually assumes some kind of structure—i.e., there is an implicit schema, but it is not enforced by the database


### id735832015
[[2024-06-19]] 16:44
> Schema-on-read is similar to dynamic (runtime) type checking in programming lan‐ guages, whereas schema-on-write is similar to static (compile-time) type checking.


### id735832965
[[2024-06-19]] 16:46
> Schema changes have a bad reputation of being slow and requiring downtime.


### id735834653
[[2024-06-19]] 16:53
> copies the entire table on ALTER TABLE, which can mean minutes or even hours of downtime when altering a large table


### id735833322
[[2024-06-19]] 16:48
> MySQL is a notable exception—it copies the entire table on ALTER TABLE, which can mean minutes or even hours of downtime when altering a large table—although various tools exist to work around this limitation


### id735839964
[[2024-06-19]] 17:06
> a schema may hurt more than it helps, and schemaless docu‐ ments can be a much more natural data model. But in cases where all records are expected to have the same structure, schemas are a useful mechanism for document‐ ing and enforcing that structure.


### id735840757
[[2024-06-19]] 17:12
> The locality advantage only applies if you need large parts of the document at the same time. The database typically needs to load the entire document, even if you access only a small portion of it, which can be wasteful on large documents. On updates to a document, the entire document usually needs to be rewritten—only modifications that don’t change the encoded size of a document can easily be per‐ formed in place [19]. For these reasons, it is generally recommended that you keep documents fairly small and avoid writes that increase the size of a document [9]. These performance limitations significantly reduce the set of situations in which document databases are useful.


### id735844034
[[2024-06-19]] 17:38
> Google’s Spanner database offers the same locality properties in a relational data model, by allowing the schema to declare that a table’s rows should be interleaved (nested) within a parent table


### id735844081
[[2024-06-19]] 17:39
> Oracle allows the same, using a feature called multi-table index cluster tables


### id735844256
[[2024-06-19]] 17:39
> column-family concept in the Bigtable data model (used in Cassandra and HBase) has a similar purpose of managing locality


### id735844425
[[2024-06-19]] 17:42
> PostgreSQL since version 9.3 [8], MySQL since version 5.7, and IBM DB2 since ver‐ sion 10.5 [30] also have a similar level of support for JSON documents. Given the popularity of JSON for web APIs, it is likely that other relational databases will follow in their footsteps and add JSON support.


## New highlights added June 19, 2024 at 6:42 PM
### id735844698
[[2024-06-19]] 17:44
> An imperative language tells the computer to perform certain operations in a certain order. You can imagine stepping through the code line by line, evaluating conditions, updating variables, and deciding whether to go around the loop one more time.
> In a declarative query language, like SQL or relational algebra, you just specify the pattern of the data you want—what conditions the results must meet, and how you want the data to be transformed (e.g., sorted, grouped, and aggregated)—but not how to achieve that goal.


### id735844703
[[2024-06-19]] 17:44
> It is up to the database system’s query optimizer to decide which indexes and which join methods to use, and in which order to execute various parts of the query.


### id735844791
[[2024-06-19]] 17:46
> Imperative code is very hard to parallelize across mul‐ tiple cores and multiple machines, because it specifies instructions that must be per‐ formed in a particular order. Declarative languages have a better chance of getting faster in parallel execution because they specify only the pattern of the results, not the algorithm that is used to determine the results.


### id735847446
[[2024-06-19]] 18:05
> MapReduce is a programming model for processing large amounts of data in bulk across many machines, popularized by Google [33]. A limited form of MapReduce is supported by some NoSQL datastores, including MongoDB and CouchDB, as a mechanism for performing read-only queries across many documents.


## New highlights added June 19, 2024 at 7:42 PM
### id735857754
[[2024-06-19]] 18:53
> The map and reduce functions are somewhat restricted in what they are allowed to do. They must be pure functions, which means they only use the data that is passed to them as input, they cannot perform additional database queries, and they must not have any side effects. These restrictions allow the database to run the functions any‐ where, in any order, and rerun them on failure. However, they are nevertheless pow‐ erful: they can parse strings, call library functions, perform calculations, and more.


## New highlights added June 20, 2024 at 9:21 AM
### id736151475
[[2024-06-20]] 08:59
> A usability problem with MapReduce is that you have to write two carefully coordi‐ nated JavaScript functions, which is often harder than writing a single query. More‐ over, a declarative query language offers more opportunities for a query optimizer to improve the performance of a query.


### id736151230
[[2024-06-20]] 08:57
> For these reasons, MongoDB 2.2 added support for a declarative query language called the aggregation pipeline


### id736153023
[[2024-06-20]] 09:06
> If your application has mostly one-to-many rela‐ tionships (tree-structured data) or no relationships between records, the document model is appropriate.


### id736153893
[[2024-06-20]] 09:09
> The rela‐ tional model can handle simple cases of many-to-many relationships, but as the con‐ nections within your data become more complex, it becomes more natural to start modeling your data as a graph.


### id736158488
[[2024-06-20]] 09:19
> A graph consists of two kinds of objects: vertices (also known as nodes or entities) and edges (also known as relationships or arcs).


## New highlights added June 20, 2024 at 10:21 AM
### id736164337
[[2024-06-20]] 09:29
> the property graph model (implemented by Neo4j, Titan, and InfiniteGraph) and the triple-store model (implemented by Datomic, AllegroGraph, and others). We will look at three declarative query lan‐ guages for graphs: Cypher, SPARQL, and Datalog. Besides these, there are also imperative graph query languages such as Gremlin [36] and graph processing frame‐ works like Pregel


## New highlights added June 20, 2024 at 5:21 PM
### id736285060
[[2024-06-20]] 16:24
> In the property graph model, each vertex consists of: • A unique identifier • A set of outgoing edges • A set of incoming edges • A collection of properties (key-value pairs)


### id736285065
[[2024-06-20]] 16:24
> Each edge consists of: • A unique identifier • The vertex at which the edge starts (the tail vertex)


### id736285078
[[2024-06-20]] 16:24
> The vertex at which the edge ends (the head vertex) • A label to describe the kind of relationship between the two vertices • A collection of properties (key-value pairs)


### id736285536
[[2024-06-20]] 16:26
> Any vertex can have an edge connecting it with any other vertex. There is no schema that restricts which kinds of things can or cannot be associated.

- [n] Seems generic to use to any entity  * [View Highlight](https://read.readwise.io/read/01j0vrnfdxk9e075dr1kswqxn3)


### id736285731
[[2024-06-20]] 16:27
> By using different labels for different kinds of relationships, you can store several different kinds of information in a single graph, while still maintaining a clean data model.

- [n] Clear label the relationship helps to provide a name for multiple relationship between the same vertexes  * [View Highlight](https://read.readwise.io/read/01j0vrq7925c3hadtftayejwhw)


### id736287872
[[2024-06-20]] 16:36
> Graphs are good for evolvability: as you add features to your application, a graph can easily be extended to accommodate changes in your application’s data structures.


### id736291276
[[2024-06-20]] 16:51
> Since SQL:1999, this idea of variable-length traversal paths in a query can be expressed using something called recursive common table expressions (the WITH RECURSIVE syntax)


## New highlights added June 20, 2024 at 6:21 PM
### id736308664
[[2024-06-20]] 17:35
> The Resource Description Framework (RDF) [41] was intended as a mechanism for different web‐ sites to publish data in a consistent format, allowing data from different websites to be automatically combined into a web of data—a kind of internet-wide “database of everything.”

- [n] Similar to mdb at Clover  * [View Highlight](https://read.readwise.io/read/01j0vwn23bf3ejcwqz6ye12gqq)


### id736308962
[[2024-06-20]] 17:36
> Triples can be a good internal data model for appli‐ cations, even if you have no interest in publishing RDF data on the semantic web.


## New highlights added June 20, 2024 at 7:21 PM
### id736320364
[[2024-06-20]] 18:52
> CODASYL’s network model

- [n] Is exactly the same as Netsuite SDF data model  * [View Highlight](https://read.readwise.io/read/01j0w10wj6nm2vwkx2hkqyp0jy)


### id736320495
[[2024-06-20]] 18:53
> Datalog’s data model is similar to the triple-store model, generalized a bit. Instead of writing a triple as (subject, predicate, object), we write it as predicate(subject, object).


## New highlights added June 20, 2024 at 10:34 PM
### id736327112
[[2024-06-20]] 19:43
> The Datalog approach requires a different kind of thinking to the other query lan‐ guages discussed in this chapter, but it’s a very powerful approach, because rules can be combined and reused in different queries. It’s less convenient for simple one-off queries, but it can cope better if your data is complex.


### id736327401
[[2024-06-20]] 19:48
> Historically, data started out being represented as one big tree (the hierarchical model), but that wasn’t good for representing many-to-many relationships, so the relational model was invented to solve that problem. More recently, developers found that some applications don’t fit well in the relational model either. New nonrelational “NoSQL” datastores have diverged in two main directions: 1. Document databases target use cases where data comes in self-contained docu‐ ments and relationships between one document and another are rare.
> 2. Graph databases go in the opposite direction, targeting use cases where anything is potentially related to everything.


### id736327666
[[2024-06-20]] 19:50
> One thing that document and graph databases have in common is that they typically don’t enforce a schema for the data they store, which can make it easier to adapt applications to changing requirements


### id736327660
[[2024-06-20]] 19:50
> your application most likely still assumes that data has a certain structure; it’s just a question of whether the schema is explicit (enforced on write) or implicit (handled on read).


### id736327696
[[2024-06-20]] 19:51
> Researchers working with genome data often need to perform sequence- similarity searches, which means taking one very long string (representing a


### id736327694
[[2024-06-20]] 19:51
> DNA molecule) and matching it against a large database of strings that are simi‐ lar, but not identical. None of the databases described here can handle this kind of usage, which is why researchers have written specialized genome database software like GenBank


### id736327817
[[2024-06-20]] 19:51
> Particle physicists have been doing Big Data–style large-scale data analysis for decades, and projects like the Large Hadron Collider (LHC) now work with hun‐ dreds of petabytes! At such a scale custom solutions are required to stop the hardware cost from spiraling out of control


### id736327821
[[2024-06-20]] 19:51
> Full-text search is arguably a kind of data model that is frequently used alongside databases.


