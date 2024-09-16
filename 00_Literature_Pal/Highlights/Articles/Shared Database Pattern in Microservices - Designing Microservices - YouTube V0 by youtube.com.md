---
title: Shared Database Pattern in Microservices - Designing Microservices - YouTube |V|0
full Title: Shared Database Pattern in Microservices - Designing Microservices - YouTube |V|0
author: youtube.com
URL: https://www.youtube.com/watch?index=4&list=PLsdq-3Z1EPT0ug8eizS71G6LZb6-4FAFt&v=tV11trlimLk
published date: 2022-04-26
category: articles
source: reader
tags: [people/pal,resource/tech,shortlist,medium/articles, author/youtube_com, reader/reader, date/2024-06-28, area/reader]
created: 2024-06-28
assignedTo: people/pal
priority: P4
work: document
---
author:: [[youtube.com]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?index=4&list=PLsdq-3Z1EPT0ug8eizS71G6LZb6-4FAFt&v=tV11trlimLk)
image_url:: [articles image URL](https://i.ytimg.com/vi/tV11trlimLk/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-06-28]]
last_highlighted_date:: [[2024-06-28]]
published_date:: [[2022-04-26]]
summary:: System Design for Beginners: https://arpitbhayani.me/sys-design
System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Microservices need to communicate with each other. Communication between them is always about getting or updating data that is owned by the other service. What if a service gets direct access to all the data it wants? This is the simplest way for the microservices to communicate with each other, and this pattern is called Sharing the Database. The core idea here is to let anyone who needs the data from a service or wants to update something, can directly talk to its database - no middlemen needed.

Although most people think it is the wrong way of communication, we should not discard it completely. In this video, we talk about what this architecture pattern is, the 4 challenges associated with it, see ways to mitigate them, and understan...


![rw-book-cover](https://i.ytimg.com/vi/tV11trlimLk/maxresdefault.jpg)

## Highlights
### id739559118
[[2024-06-28]] 10:55
> simplest way for the micro services to communicate with each other and the pattern is called sharing the database pattern


## New highlights added June 28, 2024 at 6:37 PM
### id739563995
[[2024-06-28]] 11:13
> analytic service can talk to the block service and block service can update its database


### id739563985
[[2024-06-28]] 11:13
> second approach is that analytics service has the access to the blocksdb and it can directly update the database


### id739564205
[[2024-06-28]] 11:14
> simplest way of integration no complex things required like directly two services talking to a database


### id739564271
[[2024-06-28]] 11:14
> no middleman involved so now there is no need for an analytic service to talk to block service and block service updating


### id739564361
[[2024-06-28]] 11:15
> no extra network hop your analytic service as soon as it got data can directly update it in the database so no latency overhead


### id739564391
[[2024-06-28]] 11:15
> quick development times now because analytics can directly write to the database


### id739564437
[[2024-06-28]] 11:16
> communication is happening or persistent tcp connections then someone had to manage the tcp connection pool then see your servers are scaled up see if everything works fine see if there are no network doors backlog syncs and what not


### id739564440
[[2024-06-28]] 11:16
> there no extra overhead operations are pretty simple both services talking to the same database


### id739581464
[[2024-06-28]] 12:19
> external parties are getting internal details


### id739581516
[[2024-06-28]] 12:20
> external party like it needs to get the internal schema and other implementation details like for example implement details like are they using soft deletes or heart deletes is the database normalized or not is the data redundant or not right so those kind of details


### id739708862
[[2024-06-28]] 16:42
> change the schema now analytics team needs to change their query need to change their code base to adhere to the new schema an


### id739708914
[[2024-06-28]] 16:43
> shard it or you want to move from sequel to nosql because nosql gives you by default sharding right so given that blocks team independently cannot make the decision because analytics queries


### id739710513
[[2024-06-28]] 16:46
> second challenge is sharing the database is equal to sharing the business logic so now for example to render a particular dashboard or to render a particular data onto the interface your services needs to fetch data from t1 from tables t1 t2 t3 and t4 right and this information is needed by all the three services blogs analytics and let's say a recommendation service right now the logic of logic to fetch this information is


### id739713654
[[2024-06-28]] 17:10
> losing is we are losing on cohesion what we wanted is all the services or all the components that are very tightly coupled or they were where in order to scope your micro service you should always be thinking


### id739713856
[[2024-06-28]] 17:13
> loose coupling and high cohesion the first challenge is actually breaking on loose coupling because you are having very tight coupling because they are sharing the database and the second one you are losing high cohesion because three services that seem to be tightly coupled are not and business logic needs to be changed but you cannot keep them at the same place so pretty messy situation over here so we are losing both by sharing the db
> the third challenge is risk of data corruptio


## New highlights added June 28, 2024 at 10:49 PM
### id739763656
[[2024-06-28]] 22:11
> due to a buggy script or due to a wrong script analytics ran a script and it deleted the data from the blocks tv permanently or it corrupted it


### id739763670
[[2024-06-28]] 22:12
> cascading failures and basically cascading impact across other services so here when you when you are sharing the database across multiple services you


### id739764927
[[2024-06-28]] 22:14
> challenge by sharing the database is your shared database can be abused very easily say yo


## New highlights added June 28, 2024 at 11:49 PM
### id739773425
[[2024-06-28]] 22:58
> it's a very quick solution


### id739773472
[[2024-06-28]] 22:59
> schema is not going to change to a massive extent where things are pretty stable then why not why not share the database


## New highlights added June 29, 2024 at 7:51 AM
### id739900481
[[2024-06-29]] 07:32
> read load can be moved to a replica


