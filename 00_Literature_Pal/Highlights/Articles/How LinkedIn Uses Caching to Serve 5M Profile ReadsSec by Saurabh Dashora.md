---
title: How LinkedIn Uses Caching to Serve 5M Profile Reads/Sec?
full Title: How LinkedIn Uses Caching to Serve 5M Profile Reads/Sec?
author: Saurabh Dashora
URL: 
published date: 2024-03-19
category: articles
source: reader
created: 2024-03-19
assigned to: people/pal
priority: P4
work: document
---
author:: [[Saurabh Dashora]]
note:: 
source:: [[reader]]
url:: 
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article0.00998d930354.png)
category:: [[articles]]
date:: [[2024-03-19]]
last_highlighted_date:: [[2024-03-19]]
published_date:: [[2024-03-19]]
summary:: LinkedIn has managed to handle 5 million profile reads per second with over a 99% cache hit rate using a combination of Couchbase cache, Espresso data store, and Brooklin CDC. The new architecture for profile reads at LinkedIn includes separate components for caching and data streaming, allowing for improved scalability and reduced costs. By implementing an integrated cache solution, LinkedIn achieved significant reductions in storage nodes, cost savings, and latency, demonstrating the effectiveness of their new approach.

![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article0.00998d930354.png)

## Highlights
### id695031715
[[2024-03-19]] 11:57
> 5000000 profile reads per second!

- [n] Bottleneck is the problem to handle these many reads  * [View Highlight](https://read.readwise.io/read/01hsbt9n2faxye61e5rsh6bpet)


### id695031437
[[2024-03-19]] 11:56
> • The cache hit rate was over 99%. That means 4950000 of those profile reads were served from the cache.
> • Tail latency (the latency that can have a big impact) was reduced by more than 60%

- [n] Must be 99 percentile. Cache hit rate is another metric to optimize.  * [View Highlight](https://read.readwise.io/read/01hsbt7gdpvjh7hnr1mb1nh67y)


### id695031518
[[2024-03-19]] 11:56
> Costs were down by 10

- [n] How did they reduce costs? That's interesting  * [View Highlight](https://read.readwise.io/read/01hsbt8z9c3ayapqj76q7s5d8f)


### id695032778
[[2024-03-19]] 12:02
> the Profile frontend application sent a read request to the Profile backend

- [n] Application handles some simple REST API calls  * [View Highlight](https://read.readwise.io/read/01hsbtjrv9gg80r5x2tgr1cdy0)


### id695031906
[[2024-03-19]] 11:59
> Espresso (LinkedIn’s in-house NoSQL database

- [n] NOsql database. Why profiles are stored here? Their schema can change often and it can be eventually consistent. No one with notice the difference. Document store type.  * [View Highlight](https://read.readwise.io/read/01hsbtcygde2g8wvsnvrewjfz1)


### id695031993
[[2024-03-19]] 12:00
> performed some deserialization stuff

- [n] Application, other than reading from database. Also does some serialization.  * [View Highlight](https://read.readwise.io/read/01hsbtf3n8bwmt7myaf7eym0cb)


### id695032626
[[2024-03-19]] 12:01
> the off-heap cache (OHC) on the Espresso Router.

- [n] Expresso router is used to solve the bottleneck of routing to different shards.  * [View Highlight](https://read.readwise.io/read/01hsbth769a3awmjrtq1advzk5)


### id695033245
[[2024-03-19]] 12:04
> OHC is quite efficient for hot keys but limited in scope. It had a low cache hit rate because it was local to the router instance and could only see read requests for that instance.

- [n] Bottleneck of a decentralized cache such as caffeine cache 1) it will see only cache requests to its node 2) low cache hit rate  * [View Highlight](https://read.readwise.io/read/01hsbtnvqk8gjvfcxf672ane5z)


### id695033377
[[2024-03-19]] 12:05
> adding more Espresso nodes gave diminishing returns.

- [n] Even adding more nodes would not solve the decentralized cache node problem  * [View Highlight](https://read.readwise.io/read/01hsbtrz6756fjk33yper1vnkx)


### id695033875
[[2024-03-19]] 12:06
> ![](https://substackcdn.com/image/fetch/w_2912,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa57b7dbd-5741-4be9-866c-30efd1a0d4ea_1950x1462.png)

- [n] Eraser.io was used to created this diagram  * [View Highlight](https://read.readwise.io/read/01hsbttxef5afybr7d4mxhr8v3)


