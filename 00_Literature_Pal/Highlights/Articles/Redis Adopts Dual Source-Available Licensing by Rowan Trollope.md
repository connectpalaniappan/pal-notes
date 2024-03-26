---
title: Redis Adopts Dual Source-Available Licensing
full Title: Redis Adopts Dual Source-Available Licensing
author: Rowan Trollope
URL: https://redis.com/blog/redis-adopts-dual-source-available-licensing/
published date: 2024-03-20
category: articles
source: reader
tags: [medium/articles, author/Rowan_Trollope, reader/reader, date/2024-03-22, area/reader]
created: 2024-03-25
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Rowan Trollope]]
note:: 
source:: [[reader]]
url:: [articles URL](https://redis.com/blog/redis-adopts-dual-source-available-licensing/)
image_url:: [articles image URL](https://redis.com/wp-content/uploads/2024/03/redis-dual-source-available-licensing-blog-url-preview-1200x628-1.png)
category:: [[articles]]
date:: [[2024-03-25]]
last_highlighted_date:: [[2024-03-22]]
published_date:: [[2024-03-20]]
summary:: Redis has transitioned to dual source-available licensing for future releases, combining RSALv2 and SSPLv1 licenses to provide free use of its source code. This change allows Redis to offer advanced data types and processing engines previously exclusive to Redis Stack. The new licensing approach aims to balance providing open source access while protecting the ability to invest in feature-rich products and enterprise solutions. By implementing dual licensing, Redis can continue to evolve its data platform and support its global developer community.


![rw-book-cover](https://redis.com/wp-content/uploads/2024/03/redis-dual-source-available-licensing-blog-url-preview-1200x628-1.png)

## Highlights
### id696120375
[[2024-03-21]] 20:50
> Redis has provided a foundation of performance and simplicity for the applications and data infrastructure that power the modern Internet.


### id696120345
[[2024-03-21]] 20:50
> We have already implemented dual licensing for our advanced Redis modules under the Redis Stack distribution, which has been well received by the community. In fact, more than 50% of redis.io downloads – from Redis 6 and beyond – come from Redis Stack. We now believe that extending this licensing to Redis itself will enable us to continue to evolve the most holistic set of data models, processing engines, and developer capabilities for our users.


### id696120947
[[2024-03-21]] 20:53
> Under the new license, cloud service providers hosting Redis offerings will no longer be permitted to use the source code of Redis free of charge.

- [n] Interesting how cloud providers have exploited an open source solution which has pushed the open source solution to be commercialized  * [View Highlight](https://read.readwise.io/read/01hshxrj6vstbvdsxdz2gjrhky)


### id696121426
[[2024-03-21]] 20:54
> For example, cloud service providers will be able to deliver Redis 7.4 only after agreeing to licensing terms with Redis, the maintainers of the Redis cod

- [n] All the cost for enterprise redis will be pushed to customers  * [View Highlight](https://read.readwise.io/read/01hshxthmyk8r1hp2zwxve3jkd)


### id696120346
[[2024-03-21]] 20:50
> Our dual license approach is not new; we released Redis modules (including RedisJSON, Redis Stack, etc.) under the dual licenses on Nov. 15, 2022. Now, we are moving to dual licensing for all our freely available software. We believe that the permissive approach of RSALv2 and the standard wording we use to define its limitations solve many of the challenges raised by our community.


### id696165101
[[2024-03-21]] 22:30
> we are also announcing the end of life for Redis Stack once Redis 8 is available, as a result of this change. It will no longer be necessary to provide a separate build of these capabilities as they will be part of Redis itself starting with Redis 8.

- [n] Interesting how a product is open source for a while and after it is successful it is commercialized. 
   This is similar to the point a YouTuber is made on business. Provide your product for free and on success, commercialize it.  * [View Highlight](https://read.readwise.io/read/01hsj37g1rs0aghea0w9rax3rv)


### id696120339
[[2024-03-21]] 20:49
> We strongly believe in the value of openly sharing source code and enabling practitioners to solve their problems, build communities, and create transparency. Redis provides feature-rich products to the community for free, and that development is made possible by our commercial customers who partner with us. By shifting to this license, Redis can better manage commercial uses of our source code and continue to invest in our thriving community of practitioners, some of whom are also contributors, in a manner that will not impede their work.


### id696165737
[[2024-03-21]] 22:33
> For end users who are using Redis’ open source version of Redis and new releases using either of the dual licenses for their internal or personal usage, there is no change.


### id696165745
[[2024-03-21]] 22:34
> For integration partners who built client libraries or other integrations with Redis, there is no change.


### id696165760
[[2024-03-21]] 22:34
> For commercial customers of Redis there is no change. Those customers get our technology under separately negotiated licensing terms.


### id696166226
[[2024-03-21]] 22:40
> you are building a solution that leverages Redis, but does not specifically compete with Redis itself, there is no impact.

- [n] So clearly only folks you are building commercial solutions such as memory store need to pay the money  * [View Highlight](https://read.readwise.io/read/01hsj3whbzyj888p1sp7dcheb1)


### id696120344
[[2024-03-21]] 20:50
> A “competitive offering” is a product that is sold to third parties, including through paid support arrangements, that is derived from the Redis’ code-base and significantly overlaps the capabilities of a Redis commercial product. For example, this definition would include hosting or embedding Redis as part of a solution that is sold competitively against our commercial versions of Redis (either Redis Enterprise Software or Redis Cloud). Custom licensing terms are also available to provide more clarity and enable use cases beyond the RSALv2 or SSPLv1 limitations. If you need further clarification with respect to a particular use case, you can email [redis_licensing@redis.com](mailto:redis_licensing@redis.com).


### id696166493
[[2024-03-21]] 22:45
> license change is not retroactive.

- [n] Interesting licenses can be made retroactive which can be disastrous for existing implementations  * [View Highlight](https://read.readwise.io/read/01hsj4540emtbctzxj18qnksjx)


### id696166647
[[2024-03-21]] 22:45
> we openly acknowledge that this change means Redis is no longer open source under the [OSI definition](https://opensource.org/osd/).


