---
title: Scaling Our Customer Review System for Peak Traffic
full Title: Scaling Our Customer Review System for Peak Traffic
author: Benjamin Hiltpolt
URL: https://medium.com/booking-com-development/scaling-our-customer-review-system-for-peak-traffic-cb19be434edf
published date: 2022-11-08
category: articles
source: reader
tags: [medium/articles, author/Benjamin_Hiltpolt, reader/reader, date/2024-07-30, area/reader]
created: 2024-07-30
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Benjamin Hiltpolt]]
note:: 
source:: [[reader]]
url:: [articles URL](https://medium.com/booking-com-development/scaling-our-customer-review-system-for-peak-traffic-cb19be434edf)
image_url:: [articles image URL](https://miro.medium.com/v2/resize:fit:1200/1*lzkbnnvGiq6zdLXdnFXD_w.png)
category:: [[articles]]
date:: [[2024-07-30]]
last_highlighted_date:: [[2024-07-30]]
published_date:: [[2022-11-08]]
summary:: Abstract: Customer reviews is a high-traffic system, which requires scaling to meet the peak traffic. Read on to learn how we scaled it !


![rw-book-cover](https://miro.medium.com/v2/resize:fit:1200/1*lzkbnnvGiq6zdLXdnFXD_w.png)

## Highlights
### id752394949
[[2024-07-30]] 08:57
> High availability and low latency is essential, as reviews are widely used across the booking funnel to engage our guests with the platform.


### id752395314
[[2024-07-30]] 09:00
> ands of requests per second. To achieve this scale, and with a p99 response times less than 50 ms, we serve all traffic using prematerialized and cached data.

- [n] Preprocessing, Prematerialized view and cache for good latency  * [View Highlight](https://read.readwise.io/read/01j41z01v7q72k15azfdmr0z79)


### id752397361
[[2024-07-30]] 09:10
> o prove against extreme cases like hardware failures or network problems, we also run replicas of the shards.

- [n] Replication for increased availability  * [View Highlight](https://read.readwise.io/read/01j41zm0mwtekv7xn07gb1pesn)


## New highlights added August 3, 2024 at 9:20 PM
### id753932113
[[2024-08-03]] 16:22
> One potential alternative strategy is to simply spin up an independent cluster to handle the resharding, and later replace the existing cluster.

- [n] Good idea when the organization is ready to spend on hardware  * [View Highlight](https://read.readwise.io/read/01j4d1rmhrfn9s6k9sczygwqs8)


### id753932116
[[2024-08-03]] 16:19
> Since this approach requires more hardware than the hashing algorithm, it was deemed too expensive.


### id753932698
[[2024-08-03]] 16:23
> This means we can add the necessary hardware to our datacenter and start populating those machines with their respective reviews. The property that makes it possible is referred to as monotonicity. Monotonicity means that data can only be transferred from old shards to new shards during an ongoing resharding.


### id753934993
[[2024-08-03]] 16:36
> Until the new shards have fully loaded the reassigned keys, coordinators (nodes of our routing layer) are only aware of the old scheme and route traffic only to the old shards.

- [n] Double write approach until we transition reads to the newly scheme  * [View Highlight](https://read.readwise.io/read/01j4d2qzh2ze1ydrnharepwy0w)


### id753935335
[[2024-08-03]] 16:38
> In our system’s case, it was great that years ago the teams decided to go for the Jump hash sharding algorithm.

- [n] Jump hash sharding algorithm is a good design choice  * [View Highlight](https://read.readwise.io/read/01j4d2tnj5dftwf3yp1970dyrz)


### id753936250
[[2024-08-03]] 16:39
> So whenever we introduce bigger changes, we attempt running the old and the changes systems in parallel until we can safely drop the old system.

- [n] Have proper fallbacks to learn from others mistakes  * [View Highlight](https://read.readwise.io/read/01j4d2w2asfb84nh25k3r77jy6)


