---
title: A Look at the Evolution of Benchling’s Search Architecture
full Title: A Look at the Evolution of Benchling’s Search Architecture
author: Matt Fox
URL: https://benchling.engineering/a-look-at-the-evolution-of-benchlings-search-architecture-c4d5327452c
published date: 2022-03-09
category: articles
source: reader
tags: [people/pal,resource/tech,work/document,medium/articles, author/Matt_Fox, reader/reader, date/2024-07-12, area/reader]
created: 2024-07-11
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Matt Fox]]
note:: 
source:: [[reader]]
url:: [articles URL](https://benchling.engineering/a-look-at-the-evolution-of-benchlings-search-architecture-c4d5327452c)
image_url:: [articles image URL](https://miro.medium.com/v2/resize:fit:1200/1*smWlEYzTD7M6PmEP7awWYQ.png)
category:: [[articles]]
date:: [[2024-07-11]]
last_highlighted_date:: [[2024-07-12]]
published_date:: [[2022-03-09]]
summary:: Learn about how we’ve built and iterated on our search architecture through the years!


![rw-book-cover](https://miro.medium.com/v2/resize:fit:1200/1*smWlEYzTD7M6PmEP7awWYQ.png)

## Highlights
### id744947256
[[2024-07-11]] 20:09
> give our users exactly what they need to find key insights, but slow, inconsistent, or irrelevant results can create a frustrating user experience and erode trust in the product.


### id744947437
[[2024-07-11]] 20:11
> Benchling’s initial search system was built on top of [Elasticsearch](https://www.elastic.co/what-is/elasticsearch), and we built and maintained a search index in a separate Elasticsearch cluster for each of our customers.


### id744947883
[[2024-07-11]] 20:14
> One key problem was data inconsistency between the core database and our search system.


### id744947734
[[2024-07-11]] 20:13
> We also experienced a lot of overhead in operating and maintaining this search system.


### id744947943
[[2024-07-11]] 20:15
> system executed searches as SQL queries against core tables in Postgres

- [n] Avoid consistency issue by having one source of truth  * [View Highlight](https://read.readwise.io/read/01j2j84dxswd73f4p19rzcd5zd)


### id744948844
[[2024-07-11]] 20:24
> system was designed with the assumption that the volume of searchable data per-customer would remain relatively stable.


### id744949850
[[2024-07-11]] 20:32
> use cases that made heavy use of data normalization, requiring costly joins across many tables.


### id744955527
[[2024-07-11]] 21:04
> lacked the ability to customize search functionality in Postgres for use cases that were becoming more and more common.


### id744949884
[[2024-07-11]] 20:33
> A lot of data in Benchling doesn’t looks like standard English language


### id744961187
[[2024-07-11]] 21:22
> improvements to our change data capture system, which now tracks changes at the column level — this greatly reduces re-indexing false positives.


### id744961412
[[2024-07-11]] 21:22
> along with calculated changes to our Elasticsearch cluster topology and use of performance testing


