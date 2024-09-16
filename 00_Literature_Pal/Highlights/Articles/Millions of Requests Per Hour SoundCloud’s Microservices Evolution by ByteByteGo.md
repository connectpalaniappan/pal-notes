---
title: Millions of Requests Per Hour SoundCloud’s Microservices Evolution
full Title: Millions of Requests Per Hour SoundCloud’s Microservices Evolution
author: ByteByteGo
URL: https://blog.bytebytego.com/p/millions-of-requests-per-hour-soundclouds
published date: 2024-09-03
category: articles
source: reader
tags: [technology,medium/articles, author/ByteByteGo, reader/reader, date/2024-09-05, area/reader]
created: 2024-09-05
assignedTo: people/pal
priority: P4
work: document
---
author:: [[ByteByteGo]]
note:: 
source:: [[reader]]
url:: [articles URL](https://blog.bytebytego.com/p/millions-of-requests-per-hour-soundclouds)
image_url:: [articles image URL](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F24ff4a8d-9810-41ad-aa98-897255b78bc5_1600x971.png)
category:: [[articles]]
date:: [[2024-09-05]]
last_highlighted_date:: [[2024-09-05]]
published_date:: [[2024-09-03]]
summary:: SoundCloud evolved its architecture from a monolithic design to a microservices approach to handle millions of requests per hour. They created Backends-for-Frontends (BFFs) to provide tailored API gateways for different client types, but faced challenges like complexity and code duplication. To improve efficiency, they introduced Value-Added Services and Domain Gateways, centralizing logic and enhancing service management.


![rw-book-cover](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F24ff4a8d-9810-41ad-aa98-897255b78bc5_1600x971.png)

## Highlights
### id781666889
[[2024-09-05]] 14:39
> The term BFF stands for Backends-for-Frontends. In simpler terms, think of a BFF as a dedicated API gateway for each device or interface type interacting with your application.


