---
title: How Facebook Could Have Built Threads 30X Faster & Cheaper
full Title: How Facebook Could Have Built Threads 30X Faster & Cheaper
author: Garry Tan
URL: https://youtube.com/watch?v=O2dIsZsjaBA&si=AzCNB2VCPiKkNcj9
published date: 2023-08-22
category: articles
source: reader
tags: [medium/articles, author/Garry_Tan, reader/reader, date/2024-04-02, area/reader]
created: 2024-04-01
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Garry Tan]]
note:: 
source:: [[reader]]
url:: [articles URL](https://youtube.com/watch?v=O2dIsZsjaBA&si=AzCNB2VCPiKkNcj9)
image_url:: [articles image URL](https://i.ytimg.com/vi/O2dIsZsjaBA/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGHIgRyg1MA8=&rs=AOn4CLADyIYvyve66DesDjJQ08UbxjJGfA)
category:: [[articles]]
date:: [[2024-04-01]]
last_highlighted_date:: [[2024-04-02]]
published_date:: [[2023-08-22]]
summary:: Join the upcoming beta: https://redplanetlabs.com/

What if I told you they could have made Threads with one engineer and under 10,000 lines of code, at least 30X faster and cheaper?

If they were using Rama by Red Planet Labs, they could have. This new data backend platform just dropped this week, and I think it’s one of the most important developments in software engineering in decades. 

0:00 My startup wouldn't have died
1:18 Don’t repeat yourself 
2:50 200X less person hours with autoscaling 
4:38 How it actually works 

I'm Garry Tan, President & CEO at Y Combinator. I was an engineer, designer and product manager who turned into a founder and investor, and now I want to help you in your journey to build technology that changes the world. These videos are about helping people build world-class teams and startups that touch a billion people. 

Please like this video and subscribe to my channel if you want to see more videos like this!

Follow me on Twitter and Instagram so you'll never miss my videos and id...


![rw-book-cover](https://i.ytimg.com/vi/O2dIsZsjaBA/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGHIgRyg1MA8=&rs=AOn4CLADyIYvyve66DesDjJQ08UbxjJGfA)

## Highlights
### id701096891
[[2024-04-01]] 21:45
> Watch to the end to find out exactly how a brilliant new abstraction
> for data structures means you won't be burning runway to recreate the wheel of data again and again


### id701097037
[[2024-04-01]] 21:47
> It's a totally new approach to building backend system and what Rama does is it integrates and generalizes every aspect of what it takes to build a backend system at scale and it enables you to build backends to applications in 100xless code.

- [n] Revolutionary idea to create abstraction to build backend systems  * [View Highlight](https://read.readwise.io/read/01hteb78231587gs0phpwaz9e6)


### id701097673
[[2024-04-01]] 21:48
> Each new data stack is a new code base, new set of servers, new DevOps needs and more surface area for bugs. - And so what Rama does is it enables you to build applications in fundamentally different ways.
> Because it's such a general purpose system you don't need to combine dozens of tools together. You can just use this one tool and if we look at like one piece of Rama to see like how is it possible it could be so general purpose, able to do what all these databases can do combined? You can look at how Rama does indexing.


### id701098912
[[2024-04-01]] 21:50
> we're running it with a hundred million bots posting 3,500 statuses per second at an average fan out of 403

- [n] What is the fan-out here?  * [View Highlight](https://read.readwise.io/read/01htebeqke8cnxern2vxe9h3ms)


### id701099389
[[2024-04-01]] 21:51
> Rama is D-R-Y, dry, for how you store and retrieve data


### id701099876
[[2024-04-01]] 21:56
> The programming model isn't new, but the way it integrates the pieces together has never been done before. - [Nathan] What makes Rama so powerful is how much it integrates and generalizes each of these pieces. On the left are depots. These are distributed, durable, and replicated logs of data. If you're familiar with Apache Kafka, depots are very similar except integrated with the rest of Rama. - Depots are append-only replicated logs. They're the fastest way to stream data to disk.

- [n] Append-only replicated logs which are fastest way to steam data to disk. These are distributed and replicated. And called as depots.  * [View Highlight](https://read.readwise.io/read/01htebr0brwvt0vqy6mdxy6rrj)


### id701100014
[[2024-04-01]] 21:57
> Next are ETLs, extract, transform, load topologies. These consume data from depot's in parallel to produce indexes, which we call partition states. Most of the time spent building Rama applications is spent programming ETLs, which are programmed with a pure Java API.

- [n] ETL is used to create indexes which are called partition states.  * [View Highlight](https://read.readwise.io/read/01htebtt0564c73jxa7szx2q8t)


### id701100080
[[2024-04-01]] 21:58
> PStates are how data is indexed in Rama and they're also durable and replicated.

- [n] Indexes are durable and replicated. Based on data structure instead of data models.  * [View Highlight](https://read.readwise.io/read/01htebw2kvmd8shx3vfg6741yv)


### id701100704
[[2024-04-01]] 22:01
> complex scaling operations that might happen at the app level can be brought down into the data layer and scaled automatically like the de-normalized fan out of feeds for posts going to followers

- [n] Instead of app querying and doing transformations, all the complexities is in the database.  * [View Highlight](https://read.readwise.io/read/01htec1tyvbzs7nq57pkzbv80r)


### id701100763
[[2024-04-01]] 22:04
> The first is ad hoc queries that can retrieve or aggregate data from one partition of one PState. These are called point queries.

- [n] Pstate looks similar to databases. 
   Point queries are directly query only one PState.  * [View Highlight](https://read.readwise.io/read/01htec3shxffnwr80j5pjm83at)


### id701101221
[[2024-04-01]] 22:04
> second are query topologies which are predefined queries that can look at any or all of your PStates and any or all of the partitions of your PStates.

- [n] Querying across pstates is the next type of query  * [View Highlight](https://read.readwise.io/read/01htec79zwsydpv552xeqpqspv)


### id701101432
[[2024-04-01]] 22:06
> data models. There's key value, document, column oriented, graph, and so on. A better way to think about indexing is in terms of data structures. A data model is just a specific combination of data structures. Key value is just a map. A document data model is a map of maps. Column oriented is a map of sorted maps and so on.

- [n] Wow! Learnt the difference between data model and data structure. Data model means key-value, document, column oriented, graph. Data structure is map, map of map, sorted maps and so on  * [View Highlight](https://read.readwise.io/read/01htec8xtv226ryc1nyxbexx7y)


### id701103581
[[2024-04-01]] 22:12
> PState you create can be whatever data structured combination you want and you create as many PStates as you need to support all your use cases.

- [n] Powerful to create as many data structures as you want  * [View Highlight](https://read.readwise.io/read/01htecpetks4qs64ta05x0cb1y)


### id701103750
[[2024-04-01]] 22:13
> you lose the ability to join that data across systems to do useful things.

- [n] Sharding would make you lose the ability to query across shards  * [View Highlight](https://read.readwise.io/read/01htecqwzpd6w2vcyt07mdxe91)


### id701103786
[[2024-04-01]] 22:14
> Just because you've moved a table or data to one microservice to a separate stack doesn't mean the problem is solved

- [n] Functional decomposition would not solve the scaling problem in long run  * [View Highlight](https://read.readwise.io/read/01htecsa3d2rc9ckq12n0ygz27)


### id701104317
[[2024-04-01]] 22:16
> one thing is we've released a build of Rama that anyone can try out and use. It lets you build full Rama applications and run them within a simulated cluster environment


