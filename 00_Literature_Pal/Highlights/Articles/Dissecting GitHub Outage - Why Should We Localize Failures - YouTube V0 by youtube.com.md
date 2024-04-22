---
title: Dissecting GitHub Outage - Why Should We Localize Failures? - YouTube |V|0
full Title: Dissecting GitHub Outage - Why Should We Localize Failures? - YouTube |V|0
author: youtube.com
URL: https://www.youtube.com/watch?index=13&list=PLsdq-3Z1EPT3_Z97svMs6S2y7tv1PcUmc&v=Of3FS2qDM28
published date: 2022-07-06
category: articles
source: reader
tags: [people/pal,resource/tech,medium/articles, author/youtube_com, reader/reader, date/2024-04-18, area/reader]
created: 2024-04-18
assignedTo: people/pal
priority: P4
work: document
---
author:: [[youtube.com]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?index=13&list=PLsdq-3Z1EPT3_Z97svMs6S2y7tv1PcUmc&v=Of3FS2qDM28)
image_url:: [articles image URL](https://i.ytimg.com/vi/Of3FS2qDM28/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-04-18]]
last_highlighted_date:: [[2024-04-18]]
published_date:: [[2022-07-06]]
summary:: System Design for Beginners: https://arpitbhayani.me/sys-design
System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Outages are inevitable; but we should design our architecture such that if a component is down, it should not lead to a complete outage. It is easy to say this, but hard to implement.

In this video, we dissect yet another GitHub outage, gather a few interesting insights about their Microservices architecture, and spend some time discussing and understanding the importance of having a smaller blast radius and a fool-proof way of achieving that.

Outline:

00:00 Agenda
02:36 What happened
04:30 Root Cause
05:14 Insights about their architecture
08:50 Master failover did not happen
13:40 Long-term fixes and Localizing failures

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissection...


![rw-book-cover](https://i.ytimg.com/vi/Of3FS2qDM28/maxresdefault.jpg)

## Highlights
### id708535247
[[2024-04-18]] 16:08
> if a component is down it should not lead to a complete outage a partial outage affecting few services is fine but a complete outage is catastrophic


### id708536483
[[2024-04-18]] 16:16
> discussing and understanding the importance of having a smaller blast radius and talk about a foolproof way of
> achieving that


## New highlights added April 18, 2024 at 5:11 PM
### id708536585
[[2024-04-18]] 16:19
> whenever a commit happens you have to trigger a workflow and all of that happens so a lot of jobs are asynchronous so because of this incident there was a failure or delay of some cute job for a
> period of time that's fine jobs that were cured during the incident were ran successfully after the issue was resolved this is a very important point to note so here even though their service was down when it got back up everything like the job that were queued they ran like they were put to a completion and this is a very important point around designing an architecture


## New highlights added April 18, 2024 at 10:08 PM
### id708614237
[[2024-04-18]] 21:41
> asynchronous way because that would give you fault tolerance ou

- [n] Asynchronous will give you fault tolerance out of the box  * [View Highlight](https://read.readwise.io/read/01hvt3ntbxjtx7nymedb3v77gb)


### id708614593
[[2024-04-18]] 21:45
> sharing a database looks like an empty pattern and it is indeed but a lot of people adopt it right and there is nothing wrong with it so long as if outage in one does not let your entire infrastructure go down


### id708614800
[[2024-04-18]] 21:46
> layer but we also know that let's say for database master is down a
> replica is auto promoted replica is promoted to be the master so then


### id708614925
[[2024-04-18]] 21:49
> would orchestrator do it it would rely on some metrics it would rely on some telemetry it would rely on some data that would tell it hey master is down
> let me promote a replica to be the new master someone has to do it it is not


