---
title: How Booking.com Scaled Their Customer Review System
full Title: How Booking.com Scaled Their Customer Review System
author: Quastor
URL: 
published date: 2024-07-12
category: articles
source: reader
tags: [medium/articles, author/Quastor, reader/reader, date/2024-07-16, area/reader]
created: 2024-07-16
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Quastor]]
note:: 
source:: [[reader]]
url:: 
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article3.5c705a01b476.png)
category:: [[articles]]
date:: [[2024-07-16]]
last_highlighted_date:: [[2024-07-16]]
published_date:: [[2024-07-12]]
summary:: Andrew Huberman is a professor at the Stanford School of Medicine and he runs a great podcast where he gives actionable tips on how to improve your health.


![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article3.5c705a01b476.png)

## Highlights
### id746600700
[[2024-07-15]] 23:14
> With Jump Hash, Booking.com can rely on a property called **monotonicity**. *This property states that when you add new shards to the cluster, data will only move from old shards to new shards; thus there is no unnecessary rearrangement.*

- [n] Shard rearrangement should be monotonic i.e. only in one direction  * [View Highlight](https://read.readwise.io/read/01j2wvya35s42xmqd7gtnakkst)


### id746600910
[[2024-07-15]] 23:15
> They provision the new hardware and then have coordinator nodes that figure out which keys will be remapped to the new shards and loads them.


### id746600920
[[2024-07-15]] 23:15
> The resharding process begins and the old accommodation IDs are transferred over to the new shards, but the remapped keys are not deleted from the old shards during this process.


