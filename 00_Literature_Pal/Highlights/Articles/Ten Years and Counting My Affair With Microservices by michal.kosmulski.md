---
title: Ten Years and Counting My Affair With Microservices
full Title: Ten Years and Counting My Affair With Microservices
author: michal.kosmulski
URL: https://blog.allegro.tech/2024/04/ten-years-microservices.html
published date: 2024-04-12
category: articles
source: reader
tags: [technology,medium/articles, author/michal_kosmulski, reader/reader, date/2024-07-16, area/reader]
created: 2024-07-15
assignedTo: people/pal
priority: P4
work: document
---
author:: [[michal.kosmulski]]
note:: 
source:: [[reader]]
url:: [articles URL](https://blog.allegro.tech/2024/04/ten-years-microservices.html)
image_url:: [articles image URL](https://blog.allegro.tech/img/allegro-tech.png)
category:: [[articles]]
date:: [[2024-07-15]]
last_highlighted_date:: [[2024-07-16]]
published_date:: [[2024-04-12]]
summary:: The author reflects on their ten-year journey with microservices at Allegro, highlighting the challenges and benefits of transitioning from a monolithic system. They emphasize the importance of investing in infrastructure, tooling, and learning to successfully implement microservices. Despite the complexity and auxiliary work involved, the decision to move to microservices proved worthwhile for the company's growth and scalability.


![rw-book-cover](https://blog.allegro.tech/img/allegro-tech.png)

## Highlights
### id746555349
[[2024-07-15]] 21:30
> Specific technical assumptions included:
> • focus on quality
> • microservices
> • distributed, multi-regional, active-active architecture
> • Java
> • cloud deployment
> • using open-source technologies


### id746555343
[[2024-07-15]] 21:30
> Faster development was probably the most important goal, since slow delivery was the direct reason we embarked on this long journey.


### id746556113
[[2024-07-15]] 21:34
> outline of the common architecture (service discovery, logging) created

- [n] this is called the platform  * [View Highlight](https://read.readwise.io/read/01j2wp8j8cn0cdxhcvdtjpj06s)


### id746555932
[[2024-07-15]] 21:34
> various self-service tools allowing developers to handle common tasks such as creating databases themselves rather than by involving specialized support teams

- [n] First,
   1) Do thing manually 
   2) Have a team support it 
   3) Build or identify self-service tools 
   4) Have a team manage it without any day to day activities  * [View Highlight](https://read.readwise.io/read/01j2wp6ch7fgnhtmqv5wzjtpbw)


### id746557781
[[2024-07-15]] 21:36
> while microservices themselves may be simple, the glue that holds them together is not.


### id746557801
[[2024-07-15]] 21:36
> horizontal scalability was our focus, we preferred [NoSQL databases](https://en.wikipedia.org/wiki/NoSQL) when possible

- [n] Not sure scale should be the reason for choosing NoSQL databases  * [View Highlight](https://read.readwise.io/read/01j2wpc5b1tzn7enq1dc0yzjxr)


### id746558211
[[2024-07-15]] 21:38
> This was often a significant effort even if we could divide the code in such way that the transaction or set of related operations ended up within the same service.


### id746558265
[[2024-07-15]] 21:39
> Only after a while did we learn that each database is good for some use cases and bad for others, and that we needed [polyglot persistence](https://en.wikipedia.org/wiki/Polyglot_persistence) to achieve high performance and get the required flexibility in all cases

- [n] Interesting to note the need for different databases for many use cases an application would require.  * [View Highlight](https://read.readwise.io/read/01j2wpg7f4f5wq8pr0q1cbm7hj)


### id746558417
[[2024-07-15]] 21:40
> Most of the time that’s true, but in one service we did have to switch from Cassandra to [MongoDB](https://www.mongodb.com/) after we found out our access patterns were not very well aligned with Cassandra’s data model.

- [n] Access pattern and write pattern would help determine the database based on the data model  * [View Highlight](https://read.readwise.io/read/01j2wpj9vdy9feq4ypmpgds5s2)


### id746558537
[[2024-07-15]] 21:41
> decoupling domain and persistence layers, it did help a lot in this case,

- [n] Always best practice to decouple domain and persistence layers  * [View Highlight](https://read.readwise.io/read/01j2wpm5pf63gydyfpczqwx338)


### id746558738
[[2024-07-15]] 21:43
> this situation also showed the advantage of having separate databases for each service, as only that single service experienced an outage.

- [n] Having separate database for each service would help avoid outages.  * [View Highlight](https://read.readwise.io/read/01j2wprmaqke9mvkjhk2mh393m)


### id746565582
[[2024-07-15]] 21:53
> The main point I want to make here is that using microservices has allowed us to safely experiment with various programming languages, to consciously limit the blast radius of those experiments should anything go wrong, and to perform all transitions gradually.


### id746565677
[[2024-07-15]] 21:55
> colleague suggested we split the service in two, one responsible for handling reads and the other for writes.

- [n] CQRS pattern to protect a database against spiky writes  * [View Highlight](https://read.readwise.io/read/01j2wqdcjdq1jh6fkjedxjdhxb)


### id746566050
[[2024-07-15]] 21:56
> It certainly did help, though, that both services kept being developed by the same team, and that by the time we introduced the split, the schema was already quite stable and did not change often.


