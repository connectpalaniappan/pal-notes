---
title: DragonflyDB Architecture Overview, Internals, and Trade-Offs - Hitting 6.43 Million Ops/Sec
full Title: DragonflyDB Architecture Overview, Internals, and Trade-Offs - Hitting 6.43 Million Ops/Sec
author: Arpit Bhayani
URL: https://www.youtube.com/watch?v=XbV1LoVsbME
published date: 2024-07-12
category: articles
source: reader
tags: [medium/articles, author/Arpit_Bhayani, reader/reader, date/2024-07-12, area/reader]
created: 2024-07-12
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Arpit Bhayani]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?v=XbV1LoVsbME)
image_url:: [articles image URL](https://i.ytimg.com/vi/XbV1LoVsbME/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-07-12]]
last_highlighted_date:: [[2024-07-12]]
published_date:: [[2024-07-12]]
summary:: Checkout DragonflyDB - https://www.dragonflydb.io/
DragpnflyDB Source Code - https://github.com/dragonflydb/dragonfly

System Design for SDE-2, SDE-3, and above: https://arpitbhayani.me/masterclass
System Design for Beginners: https://arpitbhayani.me/sys-design
Redis Internals: https://arpitbhayani.me/redis

PostgreSQL per-client process model - https://youtu.be/o7qLKfILuD8
PostgreSQL Internals Playlist - https://www.youtube.com/watch?v=o7qLKfILuD8&list=PLsdq-3Z1EPT1cL2FsCkxLlw-VLqK0GU-F
Database Engineering Playlist - https://www.youtube.com/watch?v=o7qLKfILuD8&list=PLsdq-3Z1EPT2C-Da7Jscr7NptGcIZgQ2l&pp=gAQBiAQB
System Design Playlist - https://www.youtube.com/watch?v=g_gKI2HCElk&list=PLsdq-3Z1EPT27BuTnJ_trF7BsaTpYLqst

### Other links

CS Engineering and Software Development books that I have read
https://arpitbhayani.me/bookshelf

Research papers that I have read
https://arpitbhayani.me/papershelf

Newsletter: https://arpit.substack.com
LinkedIn: https://linkedin.com/in/arpitbhayani
Twitter: https://twitter.c...


![rw-book-cover](https://i.ytimg.com/vi/XbV1LoVsbME/maxresdefault.jpg)

## Highlights
### id745149057
[[2024-07-12]] 10:00
> redis is single threaded while dragonfly DB is multi-threaded


### id745149438
[[2024-07-12]] 10:04
> 64 cores redis can only utilize one other 63 cores are just getting wasted


### id745149509
[[2024-07-12]] 10:05
> scale it horizontally making it a cluster to maintain the required throughput


### id745150409
[[2024-07-12]] 10:06
> unique like there's a good key distribution and you need to manage the cluster which eventually bloats up your infrastructure


