---
title: Back-of-the-envelope Estimation
full Title: Back-of-the-envelope Estimation
author: ByteByteGo
URL: https://bytebytego.com/courses/system-design-interview/back-of-the-envelope-estimation
published date: 2011-01-26
category: articles
source: reader
tags: [medium/articles, author/ByteByteGo, reader/reader, date/2024-05-15, area/reader]
created: 2024-05-14
assignedTo: people/pal
priority: P4
work: document
---
author:: [[ByteByteGo]]
note:: 
source:: [[reader]]
url:: [articles URL](https://bytebytego.com/courses/system-design-interview/back-of-the-envelope-estimation)
image_url:: [articles image URL](https://bytebytego.com/social1.png)
category:: [[articles]]
date:: [[2024-05-14]]
last_highlighted_date:: [[2024-05-15]]
published_date:: [[2011-01-26]]
summary:: Back-of-the-envelope estimation is a technique used to estimate system capacity or performance requirements in a system design interview. It involves using thought experiments and common performance numbers to estimate whether a design will meet the requirements. To carry out an effective back-of-the-envelope estimation, you need to have a good understanding of scalability basics, such as the power of two, latency numbers, and availability numbers. Being able to round and approximate, write down assumptions, and label units is also important. Commonly asked back-of-the-envelope estimations include QPS, peak QPS, storage, cache, and number of servers.


![rw-book-cover](https://bytebytego.com/social1.png)

## Highlights
### id719865758
[[2024-05-14]] 19:09
> According to Jeff Dean, Google Senior Fellow, “back-of-the-envelope calculations are estimates you create using a combination of thought experiments and common performance numbers to get a good feel for which designs will meet your requirements”


### id719866905
[[2024-05-14]] 19:26
> Power of two

- [n] 500 million users in a site uses 5KB data 
   Total storage 
   2^ 20 * 500 * 5 * 2 ^ 10 byte
   = 2500 * 2 ^ 30 bytes 
   = 2.5 * 1000 * 2^30 
   = 2.5 * 2^40 or 2500 GB 
   = 2.5 TB  * [View Highlight](https://read.readwise.io/read/01hxwt11h3ne4x2yh36z2jr3tk)


### id719866302
[[2024-05-14]] 19:15
> Although data volume can become enormous when dealing with distributed systems, calculation all boils down to the basics. To obtain correct calculations, it is critical to know the data volume unit using the power of 2. A byte is a sequence of 8 bits. An ASCII character uses one byte of memory (8 bits). Below is a table explaining the data volume unit (Table 1).
> Power
> Approximate value
> Full name
> Short name
> 10
> 1 Thousand
> 1 Kilobyte
> 1 KB
> 20
> 1 Million
> 1 Megabyte
> 1 MB
> 30
> 1 Billion
> 1 Gigabyte
> 1 GB
> 40
> 1 Trillion
> 1 Terabyte
> 1 TB
> 50
> 1 Quadrillion
> 1 Petabyte
> 1 PB

- [n] 5 million users need 1KB. 
   5 * 2 ^ 20 * 2 ^ 10 ~= 2 ^ 30 ~= 1GB of storage is needed  * [View Highlight](https://read.readwise.io/read/01hxwsjxdvkanvvg6fh4jj4z9j)


### id719866676
[[2024-05-14]] 19:17
> Dr. Dean from Google reveals the length of typical computer operations in 2010 [1]. Some numbers are outdated as computers become faster and more powerful. However, those numbers should still be able to give us an idea of the fastness and slowness of different computer operations.
> Operation name
> Time
> L1 cache reference
> 0.5 ns
> Branch mispredict
> 5 ns
> L2 cache reference
> 7 ns
> Mutex lock/unlock
> 100 ns
> Main memory reference
> 100 ns
> Compress 1K bytes with Zippy
> 10,000 ns = 10 µs
> Send 2K bytes over 1 Gbps network
> 20,000 ns = 20 µs
> Read 1 MB sequentially from memory
> 250,000 ns = 250 µs
> Round trip within the same datacenter
> 500,000 ns = 500 µs
> Disk seek
> 10,000,000 ns = 10 ms
> Read 1 MB sequentially from the network
> 10,000,000 ns = 10 ms
> Read 1 MB sequentially from disk
> 30,000,000 ns = 30 ms
> Send packet CA (California) ->Netherlands->CA
> 150,000,000 ns = 150 ms


### id719868462
[[2024-05-14]] 19:30
> By analyzing the numbers in Figure 1, we get the following conclusions:
> • Memory is fast but the disk is slow.
> • Avoid disk seeks if possible.
> • Simple compression algorithms are fast.
> • Compress data before sending it over the internet if possible.
> • Data centers are usually in different regions, and it takes time to send data between them.


### id719870973
[[2024-05-14]] 19:51
> Back-of-the-envelope estimation is all about the process. Solving the problem is more important than obtaining results. Interviewers may test your problem-solving skills. Here are a few tips to follow:
> • Rounding and Approximation. It is difficult to perform complicated math operations during the interview. For example, what is the result of “99987 / 9.1”? There is no need to spend valuable time to solve complicated math problems. Precision is not expected. Use round numbers and approximation to your advantage. The division question can be simplified as follows: “100,000 / 10”.
> • Write down your assumptions. It is a good idea to write down your assumptions to be referenced later.
> • Label your units. When you write down “5”, does it mean 5 KB or 5 MB? You might confuse yourself with this. Write down the units because “5 MB” helps to remove ambiguity.
> • Commonly asked back-of-the-envelope estimations: QPS, peak QPS, storage, cache, number of servers, etc. You can practice these calculations when preparing for an interview. Practice makes perfect.


