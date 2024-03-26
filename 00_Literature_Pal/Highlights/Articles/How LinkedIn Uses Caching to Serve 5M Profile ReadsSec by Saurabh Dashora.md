---
title: How LinkedIn Uses Caching to Serve 5M Profile Reads/Sec?
full Title: How LinkedIn Uses Caching to Serve 5M Profile Reads/Sec?
author: Saurabh Dashora
URL: 
published date: 2024-03-19
category: articles
source: reader
tags: [people/pal,medium/articles, author/Saurabh_Dashora, reader/reader, date/2024-03-22, area/reader]
created: 2024-03-25
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Saurabh Dashora]]
note:: 
source:: [[reader]]
url:: 
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article0.00998d930354.png)
category:: [[articles]]
date:: [[2024-03-25]]
last_highlighted_date:: [[2024-03-22]]
published_date:: [[2024-03-19]]
summary:: LinkedIn has managed to handle 5 million profile reads per second with over a 99% cache hit rate using a combination of Couchbase cache, Espresso data store, and Brooklin CDC. The new architecture for profile reads at LinkedIn includes separate components for caching and data streaming, allowing for improved scalability and reduced costs. By implementing an integrated cache solution, LinkedIn achieved significant reductions in storage nodes, cost savings, and latency, demonstrating the effectiveness of their new approach.


![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article0.00998d930354.png)

## Highlights
### id695031715
[[2024-03-19]] 11:57
> 5000000 profile reads per second!

- [n] Bottleneck is the problem to handle these many reads  * [View Highlight](https://read.readwise.io/read/01hsbt9n2faxye61e5rsh6bpet)


### id695031437
[[2024-03-19]] 11:56
> • The cache hit rate was over 99%. That means 4950000 of those profile reads were served from the cache.
> • Tail latency (the latency that can have a big impact) was reduced by more than 60%

- [n] Must be 99 percentile. Cache hit rate is another metric to optimize.  * [View Highlight](https://read.readwise.io/read/01hsbt7gdpvjh7hnr1mb1nh67y)


### id695031518
[[2024-03-19]] 11:56
> Costs were down by 10

- [n] How did they reduce costs? That's interesting  * [View Highlight](https://read.readwise.io/read/01hsbt8z9c3ayapqj76q7s5d8f)


### id695032778
[[2024-03-19]] 12:02
> the Profile frontend application sent a read request to the Profile backend

- [n] Application handles some simple REST API calls  * [View Highlight](https://read.readwise.io/read/01hsbtjrv9gg80r5x2tgr1cdy0)


### id695031906
[[2024-03-19]] 11:59
> Espresso (LinkedIn’s in-house NoSQL database

- [n] NOsql database. Why profiles are stored here? Their schema can change often and it can be eventually consistent. No one with notice the difference. Document store type.  * [View Highlight](https://read.readwise.io/read/01hsbtcygde2g8wvsnvrewjfz1)


### id695031993
[[2024-03-19]] 12:00
> performed some deserialization stuff

- [n] Application, other than reading from database. Also does some serialization.  * [View Highlight](https://read.readwise.io/read/01hsbtf3n8bwmt7myaf7eym0cb)


### id695032626
[[2024-03-19]] 12:01
> the off-heap cache (OHC) on the Espresso Router.

- [n] Expresso router is used to solve the bottleneck of routing to different shards.  * [View Highlight](https://read.readwise.io/read/01hsbth769a3awmjrtq1advzk5)


### id695033245
[[2024-03-19]] 12:04
> OHC is quite efficient for hot keys but limited in scope. It had a low cache hit rate because it was local to the router instance and could only see read requests for that instance.

- [n] Bottleneck of a decentralized cache such as caffeine cache 1) it will see only cache requests to its node 2) low cache hit rate  * [View Highlight](https://read.readwise.io/read/01hsbtnvqk8gjvfcxf672ane5z)


### id695033377
[[2024-03-19]] 12:05
> adding more Espresso nodes gave diminishing returns.

- [n] Even adding more nodes would not solve the decentralized cache node problem  * [View Highlight](https://read.readwise.io/read/01hsbtrz6756fjk33yper1vnkx)


### id695033875
[[2024-03-19]] 12:06
> ![](https://substackcdn.com/image/fetch/w_2912,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa57b7dbd-5741-4be9-866c-30efd1a0d4ea_1950x1462.png)

- [n] Eraser.io was used to created this diagram  * [View Highlight](https://read.readwise.io/read/01hsbttxef5afybr7d4mxhr8v3)


### id696298235
[[2024-03-22]] 07:29
> first thing to note is the Couchbase cache. It sits aside from the Espresso storage node.

- [n] LinkedIn still has the decentralized cache to defend, the centralized cache and then database. Can Proxysql take the place if Expresso router ?  * [View Highlight](https://read.readwise.io/read/01hsk24gj2ry3wrr6fz5k8d1y5)


### id696300107
[[2024-03-22]] 07:30
> Brooklin which is LinkedIn’s in-house data streaming platform.

- [n] Interesting to note the data streaming platform is used to update cache  * [View Highlight](https://read.readwise.io/read/01hsk27j1p4wveg51s9etakbjg)


### id696300245
[[2024-03-22]] 07:32
> Espresso abstracts all the caching internals and frees the developers to focus on the business logic. Hence the name Integrated Cache.

- [n] Interesting how the schema changes are added. Since it is a document store, I believe there are no joins and entire profile data is in the cache  * [View Highlight](https://read.readwise.io/read/01hsk2a4pv7qne4s0dmcz0zak0)


### id696300545
[[2024-03-22]] 07:36
> point to note was that LinkedIn initially tried to adopt memcached but the solution didn’t work well for them. Interestingly, Facebook was able to achieve massive success with memcached as we saw in an earlier post.

- [n] Memcached could have replaced couchbase. Interesting to note couchbase, a document store used as the cache  * [View Highlight](https://read.readwise.io/read/01hsk2d2yypjt4e09kd33qaam3)


### id696301558
[[2024-03-22]] 07:40
> • When the Profile backend application receives a read request, it sends the request to an Espresso router instance.
> • The router checks if the key is present in the OHC.
> • If not, the request is sent to the Couchbase cache. In case of a cache hit, the data is returned.
> • In case of a cache miss, the request is served by the storage node. The router returns the profile information to the backend
> • Lastly, the router upserts the data asynchronously into the cache.
> [![](https://substackcdn.com/image/fetch/w_2912,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff915f542-3a9d-4135-ad33-9603386e87bd_1777x1336.png)](https://substack.com/redirect/da4a3dfa-807a-4e8f-a0a5-177ad396c8f7?j=eyJ1IjoiM2kxb2pkIn0.azpX2Hg8j2Th3BsfuroTrXj1JZsT1xQcVM1pfjjyRpw)
> [You can play around with the diagram on Eraser.io](https://substack.com/redirect/6d0ca9b7-d103-4914-8ab1-abf711316e47?j=eyJ1IjoiM2kxb2pkIn0.azpX2Hg8j2Th3BsfuroTrXj1JZsT1xQcVM1pfjjyRpw)

- [n] Expresso ohc -> fallback to -> couchbase -> fallback to -> storage layer 
   Expresso update couchbase asynchronously. Note the word asynchronously.  * [View Highlight](https://read.readwise.io/read/01hsk2ktw2ymw45dmqekdb5k9j)


### id696301978
[[2024-03-22]] 07:40
> cache becomes ineffective when the data in the database changes but it’s not synced with the cache.
> To keep things in sync, they implemented a cache updater and cache bootstrapper.

- [n] Interesting way to make the cache effective  * [View Highlight](https://read.readwise.io/read/01hsk2tyjq3665w64g9p25z3ga)


### id696302144
[[2024-03-22]] 07:41
> The Brooklin change capture stream is populated with database rows committed to the database

- [n] Database row based replication  * [View Highlight](https://read.readwise.io/read/01hsk2vxq3rjwg25y4hr44yca7)


### id696302199
[[2024-03-22]] 07:54
> • The Brooklin bootstrap stream is populated with a periodically generated database snapshot.
> [![](https://substackcdn.com/image/fetch/w_2912,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F178e1ae3-6888-48b9-88ff-6de886fddca4_1777x1230.png)](https://substack.com/redirect/d2696b7e-b65f-470e-a9e4-16427f8192e9?j=eyJ1IjoiM2kxb2pkIn0.azpX2Hg8j2Th3BsfuroTrXj1JZsT1xQcVM1pfjjyRpw)
> [You can play around with the diagram on Eraser.io](https://substack.com/redirect/6d0ca9b7-d103-4914-8ab1-abf711316e47?j=eyJ1IjoiM2kxb2pkIn0.azpX2Hg8j2Th3BsfuroTrXj1JZsT1xQcVM1pfjjyRpw)

- [n] Interesting to note this has been used when a new database instance comes in.  * [View Highlight](https://read.readwise.io/read/01hsk2wmh9etztvcwv2hagt25x)


### id696302627
[[2024-03-22]] 07:43
> Guaranteed resilience in case of Couchbase failure.

- [n] Partition tolerance  * [View Highlight](https://read.readwise.io/read/01hsk2zvmpjdjrncarbs3fx2x1)


### id696302616
[[2024-03-22]] 07:43
> High-availability of cached data

- [n] Availability  * [View Highlight](https://read.readwise.io/read/01hsk2zhz37x92c6zepe1mj4dj)


### id696302773
[[2024-03-22]] 07:43
> strict service level objective on data divergence between the SOT and the cache.

- [n] Consistency  * [View Highlight](https://read.readwise.io/read/01hsk30fwgmwzr3tn6b75gp3q3)


### id696303193
[[2024-03-22]] 07:45
> Every Espresso router instance tracks the health of all Couchbase buckets it has access to. A bucket’s health is evaluated by comparing the number of request exceptions against a threshold. If a bucket is unhealthy, the router stops dispatching new requests to the bucket.

- [n] Interesting to note health check based on error rate plus availability  * [View Highlight](https://read.readwise.io/read/01hsk32vqt3ncye1rj1ysphx3z)


### id696303219
[[2024-03-22]] 07:46
> They went with 3 replicas for profile data (a leader and two followers). Every request is fulfilled by the leader. However, if the leader goes down, the router fetches data from the follower replica.

- [n] Replication. No mention whether the leader to replica updates are synchronously or asynchronously done  * [View Highlight](https://read.readwise.io/read/01hsk342ywv3mabyfjpsw1zfnk)


### id696303729
[[2024-03-22]] 07:48
> Retrying failed Couchbase requests in case the reason for failure was a router issue or a network issue. The idea is that such issues may be temporary and a retry may be successful.

- [n] Retrying once is ok for failed requests  * [View Highlight](https://read.readwise.io/read/01hsk38b0g07w3w0wt22cm3jw2)


### id696303824
[[2024-03-22]] 07:50
> Cached data must be available all the time even in the case of a datacenter failover.
> To achieve this, they cache the entire Profile dataset in every data center. It was easy for them because a typical profile payload just comes to around 24KB.

- [n] Payload size was low. Nothing was mentioned about availability???  * [View Highlight](https://read.readwise.io/read/01hsk39cf27pezxvcqpsc1qxf4)


### id696304047
[[2024-03-22]] 07:49
> TTL (Time-to-Live) for the cached data is set to a finite value to make sure any expired records get purged from the database.

- [n] Ttl was set to ensure deleted records are removed from database  * [View Highlight](https://read.readwise.io/read/01hsk3aqr9c5nbefd5tx04j6sh)


### id696304408
[[2024-03-22]] 07:52
> For each database row committed, Espresso produces a SCN value and stores it in the binlog.

- [n] Database writes are ordered with a versioning number to determine the last one  * [View Highlight](https://read.readwise.io/read/01hsk3fxgz2xn3hrybta409jnr)


### id696304266
[[2024-03-22]] 07:51
> The system follows the Last-Writer-Win (LWW) reconciliation based on the SCN value.

- [n] Conflict strategy: last writer win  * [View Highlight](https://read.readwise.io/read/01hsk3e8bz5m7pn8rvsa8h0e9t)


### id696304635
[[2024-03-22]] 07:57
> bootstrapping period is kept less than the TTL to make sure that a record present in Espresso doesn’t expire from the cache before the next bootstrapping.

- [n] Interesting strategy to bootstrap is an excellent idea to not remove any non-deleted records from the cache i.e. always have a warm cache.  * [View Highlight](https://read.readwise.io/read/01hsk3nhfsr9fg7jkykkvegnza)


### id696306578
[[2024-03-22]] 07:58
> Couchbase Compare-And-Swap (CAS) to detect concurrent updates and retry the update if necessary. Here’s

- [n] Concurrent modification handled by compare and swap  * [View Highlight](https://read.readwise.io/read/01hsk3v06f80zr5sd8k861fymw)


### id696306707
[[2024-03-22]] 07:58
> • The CAS value is typically stored alongside the data within the Couchbase server.
> • When you read data from Couchbase, the CAS value is returned with the data.
> • Then, when you perform an update operation on that data, you include the CAS value in the request.
> • If the CAS value you provide is different from the one in Couchbase, it indicates that the data has been modified by another operation.
> • In this case, you can retry the update request or handle it accordingly.
> [![](https://substackcdn.com/image/fetch/w_2912,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe32ab269-0633-4fca-9ac4-827e96376dd6_1777x1211.png)](https://substack.com/redirect/a8952f7f-8e30-4749-b0ab-151d0296edf1?j=eyJ1IjoiM2kxb2pkIn0.azpX2Hg8j2Th3BsfuroTrXj1JZsT1xQcVM1pfjjyRpw)
> [You can play around with the diagram on Eraser.io](https://substack.com/redirect/6d0ca9b7-d103-4914-8ab1-abf711316e47?j=eyJ1IjoiM2kxb2pkIn0.azpX2Hg8j2Th3BsfuroTrXj1JZsT1xQcVM1pfjjyRpw)


### id696306736
[[2024-03-22]] 07:59
> Reduction in the number of Espresso storage nodes by 90%.

- [n] Amazing cost reduction in bringing in new caches.  * [View Highlight](https://read.readwise.io/read/01hsk3x3b2j48xgerg07fmaj3t)


### id696307723
[[2024-03-22]] 08:03
> 99th percentile latency dropped by 60.73% from 31.6 ms to 12.41 ms

- [n] Latency dropped because there will always be a hit with centralized cache  * [View Highlight](https://read.readwise.io/read/01hsk42t91htm6ykgd39a5e1s9)


### id696307728
[[2024-03-22]] 08:02
> 99.9th percentile latency dropped by 63.66% from 66.87 ms to 24.3 ms.


