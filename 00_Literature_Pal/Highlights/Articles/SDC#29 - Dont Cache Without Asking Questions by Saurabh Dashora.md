---
title: SDC#29 - Don't Cache Without Asking Questions
full Title: SDC#29 - Don't Cache Without Asking Questions
author: Saurabh Dashora
URL: https://newsletter.systemdesigncodex.com/p/dont-cache-without-asking-questions
published date: 2024-02-20
category: articles
source: reader
tags: [people/pal,medium/articles, author/Saurabh_Dashora, reader/reader, date/2024-03-29, area/reader]
created: 2024-03-28
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Saurabh Dashora]]
note:: 
source:: [[reader]]
url:: [articles URL](https://newsletter.systemdesigncodex.com/p/dont-cache-without-asking-questions)
image_url:: [articles image URL](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7c644f81-e237-4856-8886-7477adbb75aa_2621x1604.png)
category:: [[articles]]
date:: [[2024-03-28]]
last_highlighted_date:: [[2024-03-29]]
published_date:: [[2024-02-20]]
summary:: Saurabh discusses key questions to consider before implementing caching in software development. He emphasizes the importance of not using caching to mask underlying issues and highlights factors like data frequency, dynamism, and caching strategy selection. Other considerations include maintaining cache consistency, deciding between cold and warm cache, and measuring cache effectiveness through metrics like hit rates and latency. Saurabh encourages thoughtful decision-making in utilizing caching solutions and invites readers to share additional questions or insights in the comments.


![rw-book-cover](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7c644f81-e237-4856-8886-7477adbb75aa_2621x1604.png)

## Highlights
### id699412944
[[2024-03-28]] 19:16
> - Am I using cache to hide the real issue?


### id699412953
[[2024-03-28]] 19:16
> , I see developers create inefficient data models and write queries that don’t use proper indexes


### id699413449
[[2024-03-28]] 19:17
> Is the data frequently accessed?


### id699413035
[[2024-03-28]] 19:17
> Fetch high-demand data without making an expensive call to the source of truth.


## New highlights added March 28, 2024 at 10:29 PM
### id699425655
[[2024-03-28]] 20:21
> Caching data that is accessed once in a while is hardly worth the trouble


### id699425668
[[2024-03-28]] 20:22
> Caching is effective when the data in your application has a bell-curve distribution when it comes to access frequency.
> See below example:
> ![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7ec4732a-0360-4d1d-a3ab-2907937fd937_1823x1039.png)


### id699429420
[[2024-03-28]] 20:47
> However, there’s one place where we can bend this rule - for data that requires heavy computation. For example, a result coming out of running an intense ML workflow. Even if the data is accessed infrequently, it’s valuable to cache it


### id699429678
[[2024-03-28]] 20:49
> Is the data dynamic?


### id699429637
[[2024-03-28]] 20:48
> You think the next time the same item is needed, you will be able to pick it up from the cache. But when the time comes, the item is gone from the cache because it was invalidated due to an update.
> **There is no advantage to caching an item that’s too dynamic.**


### id699429675
[[2024-03-28]] 20:49
> Which caching strategy should I choose


### id699429670
[[2024-03-28]] 20:48
> Some of the most popular ones are:
> • Cache-Aside or Look-Aside
> • Read-Through
> • Write-Through
> • Write-Back
> • Write-Around
> Here’s a diagram that shows how they work.
> ![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0c25f149-6b13-42c3-8ab4-5aa473bc5811_4954x5400.png)


### id699429654
[[2024-03-28]] 20:48
> Choosing a strategy before you start is important as it will impact other parameters such as **consistency, latency and performance**


### id699429916
[[2024-03-28]] 20:50
> How will I maintain cache consistency?


### id699429920
[[2024-03-28]] 20:50
> Cache invalidation is one of the hardest problems in computer science


### id699429891
[[2024-03-28]] 20:50
> why do you need to invalidate an item in the cache?
> To maintain **cache consistency**


### id699429957
[[2024-03-28]] 20:51
> you can code your application to invalidate a cache item whenever it updates the source database. But in a distributed environment with replica regions, you don’t want invalidations to happen before the replication. Otherwise, there are chances of stale data


### id699430021
[[2024-03-28]] 20:52
> , in a highly


### id699430042
[[2024-03-28]] 20:52
> concurrent environment with multiple clients trying to establish cache consistency, which client should get the honor?
> If you don’t choose an appropriate strategy, you may have a **cache stampede/thundering herd** on your hands.
> ![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F18d06bc0-4593-403a-9bf1-e2357e482892_4816x5345.png)


### id699430258
[[2024-03-28]] 20:53
> Cold Cache or Warm Cache?


### id699430315
[[2024-03-28]] 20:53
> cold cache takes time to reach a good performance level. During that time, many requests will hit the database or the disk


### id699430477
[[2024-03-28]] 20:53
> In a highly concurrent environment, a cold cache can cause cascading failures due to excessive load on the backend and the database. So, it might be better to go for a warm cache.
> But for that, you need to create a strategy to pre-cache data based on the expected demand. It might be a costly effort.


