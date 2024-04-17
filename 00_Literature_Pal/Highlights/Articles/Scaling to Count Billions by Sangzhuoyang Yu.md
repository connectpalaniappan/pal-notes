---
title: Scaling to Count Billions
full Title: Scaling to Count Billions
author: Sangzhuoyang Yu
URL: https://www.canva.dev/blog/engineering/scaling-to-count-billions/
published date: 2024-04-12
category: articles
source: reader
tags: [medium/articles, author/Sangzhuoyang_Yu, reader/reader, date/2024-04-15, area/reader]
created: 2024-04-15
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Sangzhuoyang Yu]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.canva.dev/blog/engineering/scaling-to-count-billions/)
image_url:: [articles image URL](https://www.canva.dev/icon-192x192.png)
category:: [[articles]]
date:: [[2024-04-15]]
last_highlighted_date:: [[2024-04-15]]
published_date:: [[2024-04-12]]
summary:: How we built a scalable and reliable content usage counting service.


![rw-book-cover](https://www.canva.dev/icon-192x192.png)

## Highlights
### id707275338
[[2024-04-15]] 18:40
> How we built a scalable and reliable content usage counting service.


### id707275607
[[2024-04-15]] 18:43
> • Accuracy. The usage count should never be wrong, and we want to minimize issues such as data loss and overcounting because the income and trust of content creators are at stake.
> • Scalability. We need to store and process usage data with this large volume and exponential growth over time.
> • Operability. As usage data volume grows, the operational complexity of regular maintenance, incident handling, and recovery also increases.

- [n] Functional requirements or principles for the design of the counting service  * [View Highlight](https://read.readwise.io/read/01hvj282rk3grqqhx568tyfnwm)


### id707275653
[[2024-04-15]] 18:44
> The Solution
> ![](https://www.canva.dev/_next/static/media/final.abe03387.png)
> Our latest architecture with OLAP database
> *Our latest architecture with OLAP database.*
> The previous diagram shows our latest architecture, which incorporates:
> • Moving away from OLTP (Online Transaction Processing) databases, to OLAP (Online Analytical Processing) databases, which provide scalable storage and computing.
> • Moving away from using scheduled worker services for calculation, to using an ELT (Extract, Load, Transform) pipeline leveraging OLAP databases to perform end-to-end calculations.

- [n] Scalable storage and computing. Better to use olap database vs oltp database  * [View Highlight](https://read.readwise.io/read/01hvj29y5xgzgc1nhxpwmjvn5a)


## New highlights added April 16, 2024 at 11:30 PM
### id707711140
[[2024-04-16]] 22:51
> Start with MySQL
> ![](https://www.canva.dev/_next/static/media/initial.6687fa4f.png)
> Our initial architecture using MySQL
> *Our initial architecture using MySQL.*
> We started with the tech stack we were most familiar with, MySQL, and built major components separately using worker services. We also persisted multiple layers of reusable intermediary output. For example, the deduplication worker scanned the deduplicated usage table and updated every record by matching each of them with an event type. We then aggregated the results by scanning the updated deduplication table and incrementing the counter persisted in another table. This architecture worked well up to a point, with 3 issues: processing scalability, incident handling, and storage consumption.


