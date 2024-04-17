---
title: Maximizing Cloud SQL Database Availability
full Title: Maximizing Cloud SQL Database Availability
author: Google Cloud Tech
URL: https://www.youtube.com/watch?v=SfHdBLGyR9U
published date: 2024-04-09
category: articles
source: reader
tags: [medium/articles, author/Google_Cloud_Tech, reader/reader, date/2024-04-15, area/reader]
created: 2024-04-15
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Google Cloud Tech]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?v=SfHdBLGyR9U)
image_url:: [articles image URL](https://i.ytimg.com/vi/SfHdBLGyR9U/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-04-15]]
last_highlighted_date:: [[2024-04-15]]
published_date:: [[2024-04-09]]
summary:: Rahul discusses maximizing Cloud SQL availability, highlighting common causes of downtime and advancements in near-zero downtime maintenance. Cloud SQL's sub-second downtime and advanced Disaster Recovery features ensure high availability, benefiting applications like generative AI in critical industries. Additional resources can be found in the Cloud SQL documentation for in-depth information on maximizing database availability.


![rw-book-cover](https://i.ytimg.com/vi/SfHdBLGyR9U/maxresdefault.jpg)

## Highlights
### id707258934
[[2024-04-15]] 16:50
> are we able to achieve this subc downtime so the way that we do it is uh what we are what we're doing in under the hood is we are creating what we call as a shadow replica and we make sure that the replica is fully caught up with the primary instance and as soon as that happens we just do a quick cut over and you know the we start redirecting the traffic to the new primary instance and to the application and to the user it seems like nothing really happened ther

- [n] Shadow replica with the replication fully caught up and a sub second switcher over to the new primary which was earlier the shadow replica. Total downtime would be sub-seconds.  * [View Highlight](https://read.readwise.io/read/01hvhvqrde448dcdmfmbecdvr8)


