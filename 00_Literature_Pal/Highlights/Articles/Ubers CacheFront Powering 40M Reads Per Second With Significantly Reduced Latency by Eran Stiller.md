---
title: Uber's CacheFront Powering 40M Reads Per Second With Significantly Reduced Latency
full Title: Uber's CacheFront Powering 40M Reads Per Second With Significantly Reduced Latency
author: Eran Stiller
URL: https://www.infoq.com/news/2024/02/uber-cachefront/?utm_campaign=infoq_content&utm_source=infoq&utm_medium=feed&utm_term=global
published date: 2024-02-29
category: articles
source: reader
created: 2024-03-17
assigned to: people/pal
priority: P4
work: document
---
author:: [[Eran Stiller]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.infoq.com/news/2024/02/uber-cachefront/?utm_campaign=infoq_content&utm_source=infoq&utm_medium=feed&utm_term=global)
image_url:: [articles image URL](https://res.infoq.com/news/2024/02/uber-cachefront/en/headerimage/CacheFront-Cover-1709203664304.jpg)
category:: [[articles]]
date:: [[2024-03-17]]
last_highlighted_date:: [[2024-03-18]]
published_date:: [[2024-02-29]]
summary:: Uber developed an innovative caching solution, CacheFront, for its in-house distributed database, Docstore. CacheFront enables over 40M reads per second from online storage and achieves substantial performance improvements, including a 75% reduction in P75 latency and over 67% reduction in P99.9 latency, demonstrating its effectiveness in enhancing system efficiency and scalability. By Eran Stiller

![rw-book-cover](https://res.infoq.com/news/2024/02/uber-cachefront/en/headerimage/CacheFront-Cover-1709203664304.jpg)

## Highlights
### id694335263
[[2024-03-17]] 22:19
> Some teams at Uber used [Redis](https://redis.io/) caching to speed up read access and overcome these limitations. However, each team has to provision and maintain their own Redis cache for their respective services. They also had to implement their invalidation logic for its use case. In a region failover, teams must either maintain caching replication to stay hot or suffer higher latencies while the cache is warming up in other regions. One of CacheFront's goals was to centrally implement and manage these features, allowing teams to focus on their core logic.


### id694335262
[[2024-03-17]] 22:19
> Uber's engineers leveraged Docstore's integrated [Change Data Capture](https://en.wikipedia.org/wiki/Change_data_capture) (CDC) engine to handle cache invalidation. Whenever the CDC identifies a DB update, the correlating row in Redis is either updated or invalidated. As a result, Uber can make the cache consistent within seconds of the database change, as opposed to minutes, by using standard Time-to-Live (TTL) mechanisms. Additionally, by using CDC, uncommitted transactions don't pollute the cache.


