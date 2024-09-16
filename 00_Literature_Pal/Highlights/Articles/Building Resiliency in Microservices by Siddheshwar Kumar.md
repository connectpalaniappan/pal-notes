---
title: Building Resiliency in Microservices
full Title: Building Resiliency in Microservices
author: Siddheshwar Kumar
URL: https://rai-skumar.medium.com/building-resiliency-in-microservices-296c4daf77c8?source=rss-b737090305c3------2
published date: 2023-07-27
category: articles
source: reader
tags: [people/pal,medium/articles, author/Siddheshwar_Kumar, reader/reader, date/2024-06-30, area/reader]
created: 2024-06-30
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Siddheshwar Kumar]]
note:: 
source:: [[reader]]
url:: [articles URL](https://rai-skumar.medium.com/building-resiliency-in-microservices-296c4daf77c8?source=rss-b737090305c3------2)
image_url:: [articles image URL](https://miro.medium.com/v2/resize:fit:571/1*aljczU6asAfOmc4-xnpVbg.png)
category:: [[articles]]
date:: [[2024-06-30]]
last_highlighted_date:: [[2024-06-30]]
published_date:: [[2023-07-27]]
summary:: Gone are the days when applications used to be two or three tier (web, app and DB). Now we have tens (and in some cases even hundreds) of interlinked services and most with their own databases. All these components (or subsystems) stack together to serve end users. A fault in one of the service sitting 5 (http) calls away (from a user) could cascade all the way up and result in a failure. This is where resiliency becomes important. Let’s see the literal meaning of Resilience.Resilience: the capacity to withstand or to recover quickly from difficulties.A resilient microservice would be able to withstand some of the faults in itself or its dependencies. So it’s a measure of how many faults (or for how long) the service can tolerate before becoming non-usable.“Ability to provide and maintain an acceptable level of service in the face of faults and challenges to normal operation.” — wikipediaBelow are two examples of resilient services.What if the service gets double the load than it is expected to serve? If the ser...


![rw-book-cover](https://miro.medium.com/v2/resize:fit:571/1*aljczU6asAfOmc4-xnpVbg.png)

## Highlights
### id740479432
[[2024-06-30]] 18:45
> fault in one of the service sitting 5 (http) calls away (from a user) could cascade all the way up and result in a failure. This is where resiliency becomes importa


### id740479416
[[2024-06-30]] 18:45
> **Resilience**: the capacity to withstand or to recover quickly from difficulties.


### id740480037
[[2024-06-30]] 18:46
> “Ability to provide and maintain an acceptable level of service in the face of faults and challenges to normal operation.” — [wikipedia](https://en.wikipedia.org/wiki/Resilience_(network))


### id740480062
[[2024-06-30]] 18:46
> What if the service gets double the load than it is expected to serve? If the service is resilient then it might slow down, might start failing fast if it can’t handle request within allowed time but it should recover once the load comes back to normal level.


### id740480124
[[2024-06-30]] 18:48
> What happens if one of the node (out of 10) goes down? Now each instance gets roughly 10% more traffic. Does it lead to collapse of the whole system or it can withstand the extra load while you try to add the node back to the cluster.


## New highlights added July 1, 2024 at 6:38 PM
### id740783660
[[2024-07-01]] 15:19
> **Timeouts**
> > Timeout is a mechanism to stop waiting for response from a service if you think it won’t come. It can help in *fault isolation,* as a dependency problem shouldn’t become a caller’s problem. And timeouts are not only relevant for network calls, resource pool that block threads must have a timeout to ensure that calling thread unblocks if the resource is not available.


### id740783791
[[2024-07-01]] 15:20
> If you wait too long on a web page, the user might give up the hope and refresh the page, causing an additional inbound request. Every external API call should have a fixed timeout, and it should be validated and updated with changes in system behavior


