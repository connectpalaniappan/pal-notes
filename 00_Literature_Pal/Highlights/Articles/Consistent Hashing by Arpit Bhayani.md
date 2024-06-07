---
title: Consistent Hashing
full Title: Consistent Hashing
author: Arpit Bhayani
URL: https://arpitbhayani.me/blogs/consistent-hashing
published date: 2020-05-24
category: articles
source: reader
tags: [author/arpit_preread,people/pal,resource/tech,medium/articles, author/Arpit_Bhayani, reader/reader, date/2024-05-25, area/reader]
created: 2024-06-02
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Arpit Bhayani]]
note:: 
source:: [[reader]]
url:: [articles URL](https://arpitbhayani.me/blogs/consistent-hashing)
image_url:: [articles image URL](https://edge.arpitbhayani.me/img/covers/general-cover.jpg)
category:: [[articles]]
date:: [[2024-06-02]]
last_highlighted_date:: [[2024-05-25]]
published_date:: [[2020-05-24]]
summary:: Consistent Hashing is one of the most sought after techniques when it comes to designing highly scalable distributed systems. In this article, we dive deep into the need for Consistent Hashing, the internals of it, and more importantly alon


![rw-book-cover](https://edge.arpitbhayani.me/img/covers/general-cover.jpg)

## Highlights
### id724405213
[[2024-05-25]] 14:25
> The core concept of Consistent Hashing was introduced in the paper [Consistent Hashing and RandomTrees: Distributed Caching Protocols for Relieving Hot Spots on the World Wide Web](https://www.akamai.com/us/en/multimedia/documents/technical-publication/consistent-hashing-and-random-trees-distributed-caching-protocols-for-relieving-hot-spots-on-the-world-wide-web-technical-publication.pdf) but it gained popularity after the famous paper introducing DynamoDB - [Dynamo: Amazon’s Highly](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf)


### id724405214
[[2024-05-25]] 14:25
> The two famous examples that exhaustively use this technique are Bit Torrent, for their peer-to-peer networks and Akamai, for their web caches.


### id724405215
[[2024-05-25]] 14:25
> A good hash function has the following properties
> • The function is computationally efficient and the values generated are easy for lookups
> • The function, for most general use cases, behaves like a pseudorandom generator that spreads data out evenly without any noticeable correlation


### id724405239
[[2024-05-25]] 14:26
> Consistent Hashing addresses this situation by keeping the Hash Space huge and constant, somewhere in the order of `[0, 2^128 - 1]` and the storage node and objects both map to one of the slots in this huge Hash Space. Unlike in the traditional system where the file was associated with storage node at index where it got hashed to, in this system the chances of a collision between a file and a storage node are infinitesimally small and hence we need a different way to define this association.


