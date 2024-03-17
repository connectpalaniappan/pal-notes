---
title: Patterns of Enterprise Application Architecture (Addison-Wesley Signature Series (Fowler))
full Title: Patterns of Enterprise Application Architecture (Addison-Wesley Signature Series (Fowler))
author: Martin Fowler
note: 
URL: 
published date: 
category: books
source: kindle
note created: 2024-03-14
assigned to: people/pal
priority: P4
work: document
---
author:: [[Martin Fowler]]
note:: 
source:: [[kindle]]
url:: 
image_url:: [books image URL](https://images-na.ssl-images-amazon.com/images/I/51X%2Br%2BOdV3L._SL200_.jpg)
category:: [[books]]
date:: [[2024-03-14]]
last_highlighted_date:: [[2018-04-21]]
published_date:: [[]]
summary:: None

![rw-book-cover](https://images-na.ssl-images-amazon.com/images/I/51X%2Br%2BOdV3L._SL200_.jpg)

## Highlights
### Location 537
[[2018-04-20]] 23:56
> Response time is the amount of time it takes for the system to process a request from the outside. This may be a UI action, such as pressing a button, or a server API call.


### Location 539
[[2018-04-20]] 23:56
> Responsiveness is about how quickly the system acknowledges a request as opposed to processing it.


### Location 543
[[2018-04-20]] 23:56
> Latency is the minimum time required to get any form of response, even if the work to be done is nonexistent.


### Location 547
[[2018-04-20]] 23:56
> Throughput is how much stuff you can do in a given amount of time.


### Location 556
[[2018-04-20]] 23:56
> Load sensitivity is an expression of how the response time varies with the load.


### Location 559
[[2018-04-20]] 23:56
> Efficiency is performance divided by resources.


### Location 560
[[2018-04-20]] 23:56
> The capacity of a system is an


### Location 561
[[2018-04-20]] 23:56
> indication of maximum effective throughput or load.


### Location 571
[[2018-04-20]] 23:56
> When building enterprise systems, it often makes sense to build for hardware scalability rather than capacity or even efficiency.


### Location 792
[[2018-04-20]] 23:56
> The more pure HTML you can go, the easier life is.


### Location 797
[[2018-04-20]] 23:56
> favor of the Web presentation


### Location 799
[[2018-04-20]] 23:56
> all on the server is the best choice for ease of maintenance.


### Location 805
[[2018-04-20]] 23:56
> Splitting across both the desktop and the server sounds like the worst of both worlds because you don’t know where any piece of logic may be.


### Location 810
[[2018-04-20]] 23:56
> Don’t try to separate the layers into discrete processes unless you absolutely have to.


### Location 813
[[2018-04-20]] 23:56
> complexity boosters—distribution, explicit multithreading, paradigm chasms (such as object/relational), multiplatform development, and extreme performance requirements (such as more than 100 transactions per second). All


### Location 860
[[2018-04-20]] 23:56
> strategy object creates the results.


### Location 935
[[2018-04-20]] 23:56
> As well as providing a clear API, the Service Layer (133) is also a good spot to place such things as transaction control and security.


### Location 1097
[[2018-04-20]] 23:56
> Unit of Work (184) is as an object that acts as the controller of the database mapping.


### Location 1102
[[2018-04-20]] 23:56
> keep a record of every row you read in an Identity Map


### Location 1111
[[2018-04-20]] 23:56
> on. Lazy Load (200) relies on having a placeholder for a reference to an object.


### Location 1137
[[2018-04-20]] 23:56
> databases are optimized to handle up to three or four joins per query.


### Location 2324
[[2018-04-20]] 23:56
> A Transaction Script organizes all this logic primarily as a single procedure, making calls directly to the database or through a thin database wrapper.


### Location 2332
[[2018-04-20]] 23:56
> Where you put the Transaction Script will depend on how you organize your layers.


### Location 2352
[[2018-04-20]] 23:56
> Domain Model (116) will give you many more options in structuring the code, increasing readability and decreasing duplication.


