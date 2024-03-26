---
title: SDC#27 - Facebook's Memcache Breakdown
full Title: SDC#27 - Facebook's Memcache Breakdown
author: Saurabh Dashora
URL: https://newsletter.systemdesigncodex.com/p/facebook-memcache-breakdown
published date: 2024-02-06
category: articles
source: reader
tags: [people/pal,medium/articles, author/Saurabh_Dashora, reader/reader, date/2024-03-24, area/reader]
created: 2024-03-25
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Saurabh Dashora]]
note:: 
source:: [[reader]]
url:: [articles URL](https://newsletter.systemdesigncodex.com/p/facebook-memcache-breakdown)
image_url:: [articles image URL](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F03fc5cae-f17b-4c52-b12b-12f5747e76a4_2751x1624.png)
category:: [[articles]]
date:: [[2024-03-25]]
last_highlighted_date:: [[2024-03-24]]
published_date:: [[2024-02-06]]
summary:: Facebook's Memcache Breakdown details how Facebook tackled challenges in handling user requests and data across its global network. The company adopted Memcache to support real-time communication, content aggregation, and to scale its systems for billions of user requests. Memcache played a crucial role in reducing database load by serving as a query cache and a generic key-value store. Facebook implemented strategies like leasing to manage issues such as stale data sets and thundering herds, and utilized techniques like consistent hashing and UDP requests to optimize performance and reduce latency. Additionally, the document outlines how Facebook addressed failures through automated remediation systems and the use of dedicated "Gutter" machines to ensure system resilience during outages.


![rw-book-cover](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F03fc5cae-f17b-4c52-b12b-12f5747e76a4_2751x1624.png)

## Highlights
### id697004406
[[2024-03-23]] 17:15
> social network cannot go down. Period.

- [n] Even social network cannot go down. It's strength and weakness is that everyone is connected. More people want to connect, they join the social network. People want to leave, the entire group leaves.  * [View Highlight](https://read.readwise.io/read/01hspp17d9pzaxe6rmvh34j5zt)


### id697082336
[[2024-03-23]] 22:56
> **Facebook’s paper on Scaling Memcache** provides a great sneak peak into the inner workings of the world’s most popular social network. Though it was published many years ago, the learnings from the paper are still relevant for software engineers at all levels.


### id697036833
[[2024-03-23]] 19:25
> Facebook needed *almost* real-time communication

- [n] Network  * [View Highlight](https://read.readwise.io/read/01hspxhzd9amtfv0vgg469a2g9)


### id697036427
[[2024-03-23]] 19:24
> On-the-fly content aggregation

- [n] Compute  * [View Highlight](https://read.readwise.io/read/01hspxgz63pkjx9gsavfqypv11)


### id697036386
[[2024-03-23]] 19:24
> Store trillions of items across multiple geographic locations

- [n] Storage  * [View Highlight](https://read.readwise.io/read/01hspxggvzww077769be3etm7z)


### id697036976
[[2024-03-23]] 22:56
> As mentioned earlier, the open-source version provided a single machine in-memory hash table. Facebook took this version as a basic building block and created a distributed key-value store known as Memcache.

- [n] Memcached is not distributed whereas memcached is distributed  * [View Highlight](https://read.readwise.io/read/01hspxkkbrqp96v90rrt14y9py)


### id697080053
[[2024-03-23]] 22:40
> reduce the **read load** on the databases


### id697080069
[[2024-03-23]] 22:41
> **Demand filled”** because the data gets into the cache only when it’s requested.

- [n] Demand filled is one way to load cache  * [View Highlight](https://read.readwise.io/read/01hsq8qr6ts0sxftxb8hknywa6)


### id697081465
[[2024-03-23]] 22:52
> **Look aside”** because they first check the cache and go to the database only in case of a miss


### id697082318
[[2024-03-23]] 22:56
> The below diagram shows what a **demand-filled look-aside cache** looks like:
> ![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F03fc5cae-f17b-4c52-b12b-12f5747e76a4_2751x1624.png)


### id697081646
[[2024-03-23]] 22:52
> Facebook also uses Memcache as a more general purpose key-value store.


### id697081651
[[2024-03-23]] 22:52
> Teams can store **pre-computed** results from ML algorithms into Memcache. These results can then be accessed by other applications when needed


### id697082267
[[2024-03-23]] 22:55
> • **Region -** These are basically global locations where Facebook servers are located. There is a **Primary** region and multiple **Secondary** regions. Each region consists of **multiple frontend clusters** and only **one storage cluster**.
> • **Frontend Cluster** - Consists of multiple web servers and memcache servers.


### id697082287
[[2024-03-23]] 22:55
> **Storage Cluster -** This contains the **source-of-truth** database that holds the authoritative copy of every data item.


### id697082289
[[2024-03-23]] 22:56
> The below diagram shows the high-level view of the architecture:
> ![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0a1ff89f-af0a-4d69-bb45-987ccbfbffb0_2751x1624.png)
> [You can play around with the diagram on Eraser.io](https://app.eraser.io/workspace/TqbJvU0x9TiiX1Elt2IY?origin=share)


### id697082405
[[2024-03-23]] 22:58
> Willingness to expose slightly stale data instead of allowing excessive load on the backend.

- [n] An excellent tradeoff to have cache  * [View Highlight](https://read.readwise.io/read/01hsq9q3v848zfvfbrwt170s31)


### id697082474
[[2024-03-23]] 22:58
> Ultimately, they don’t want to risk availability.


### id697082524
[[2024-03-23]] 22:59
> Every frontend cluster has hundreds of Memcached servers and items are distributed across these servers using **Consistent Hashing**

- [n] Consistent hashing is used  * [View Highlight](https://read.readwise.io/read/01hsq9sv3wj2gh0z9nbwa92d4p)


### id697082338
[[2024-03-23]] 22:56
> In other words, one request means webservers must communicate with many Memcached servers in a short period of time. And mind you, this is applicable for both **cache hit** and **cache miss** scenarios.


### id697082334
[[2024-03-23]] 22:56
> As we discussed earlier, one region at Facebook consists of **multiple frontend clusters** but **only one storage cluster**. And each frontend cluster consists of multiple webservers and Memcached servers.


### id697082335
[[2024-03-23]] 22:56
> Users may connect to different frontend cluster when requesting for data depending on how those requests are load-balanced. This ends up caching the data in multiple clusters.


### id697082331
[[2024-03-23]] 22:56
> This provides **read-after-write** consistency for the user that made the request. It also reduces the time that stale data exists within the cluster after the data has been updated.


