---
title: The Architecture of DoorDash's Search Engine
full Title: The Architecture of DoorDash's Search Engine
author: Quastor
URL: 
published date: 2024-03-19
category: articles
source: reader
created: 2024-03-19
assigned to: people/pal
priority: P4
work: document
---
author:: [[Quastor]]
note:: 
source:: [[reader]]
url:: 
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article1.be68295a7e40.png)
category:: [[articles]]
date:: [[2024-03-19]]
last_highlighted_date:: [[2024-03-19]]
published_date:: [[2024-03-19]]
summary:: This change (along with growth in the number of stores/restaurants) meant that the company needed to quickly scale their search system.

![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article1.be68295a7e40.png)

## Highlights
### id695121895
[[2024-03-19]] 16:53
> We'll talk about Apache Lucene and how DoorDash built a Search Engine using it. Plus, Hashing explained with interactive graphics, curated resources on debuggers and more.


### id695121894
[[2024-03-19]] 16:53
> This change (*along with growth in the number of stores/restaurants*) meant that the company needed to quickly scale their search system. Restaurants can each sell tens/hundreds of different dishes and these *all* need to be indexed.


### id695121884
[[2024-03-19]] 16:53
> **Customization** - Elasticsearch didn’t have enough support for modeling complex document relationships. Additionally, it didn’t have enough features for query understanding and ranking.


### id695121887
[[2024-03-19]] 16:53
> To solve this, the DoorDash team decided to build their own search engine. They built it using Apache Lucene but customized the indexing and searching processes based on their own specification. They published a fantastic [blog post](https://link.mail.beehiiv.com/ss/c/u001.LUZYrxblx92g0_IcD8eBHeJtYbs4ot4RMUOF7cLoZ2CScIMZ4UtCcNpQOxTTupf_Mt10pdLdD20D6efLpreEygxB6yIXpWoVOyWBl4SIZbxiy_VAsSJ71KU64zFAEMt-HRu5NyIIerv5D0EWZmKFyE9k_mbRwdkoGHpVtIxCJJQxOo6c_4qwfkjGXXfbbRLCb2rftJuWdsqdR9DdRmospu07Rf-aD15-jVsqCAK2OoQ6cW-ugnLcUVpfm-Pz4R-NMLmIq3O-E2pbICWExl2UNQ/44s/Zoprns6vSCeJTQQgYag-GA/h8/h001.Pg32SNRkj4XDfWZVuBSV7c0ahw9KyDks2xDyhQOaX2o) on how they did it.


### id695121885
[[2024-03-19]] 16:53
> Lucene is a high-performance library for *building* search engines. It’s written in 1999 by Doug Cutting (*he later co-founded Apache Hadoop*) based on work he did at Apple, Excite and Xerox PARC.


### id695121902
[[2024-03-19]] 16:53
> **Search** - Lucene can parse query strings and search for them against the index of documents. It has different search algorithms and also provides capabilities for ranking results by relevance.


### id695121904
[[2024-03-19]] 16:53
> DoorDash used components of Lucene for their own search engine. However, they also designed their own indexer and searcher based on their personal specifications.


### id695121900
[[2024-03-19]] 16:53
> **Indexing Documents** - taking any new documents (*or updates*) and processing them into a format so their text can be searched through quickly. A very common structure is the [inverted index format](https://link.mail.beehiiv.com/ss/c/u001.Bc-x3nagLtH0LbJG9-uKVQHIp7sFlNX1_5SOzQf3bGgGrWNVp0EY_mwcJqqv8NTC24nv7A-lAKIIobc5VHzGJbZQQfo9c4HvVRkvSyfAzdTxwPGA9MN3dh7ptyWNj4L2Q1NQffndkhpDhj1Hj-7ypVM0C71KEmjNiO5vyqWIK5bKLrDHKc2gBbkm7rflg0M3RmfpUdAfjuXjxC9qvMbVnZFPZW_yDjPArakleOZzKxAvjGn1jQzmxH575Nt_5x7VLBurxswXfA5X1V9WRx_Hy3YoX6ghbPNCdeJUlmpdbYrMy2QBv7CN8uvNyiwLL-ohXQUaF_O-oTDFHviCcTOsdg/44s/Zoprns6vSCeJTQQgYag-GA/h11/h001.51F7Gn-lg4tjTB-uyUxPEGpswV4gU7fy9jsc0YK-KKw), that’s similar to the index section in the back of a textbook. Lucene uses an [inverted index](https://link.mail.beehiiv.com/ss/c/u001.4_sem6LoN8nYZowj70JzKdOmbtIU7JnAn0YweBYXpMXvMDsphElrdApTyb6D8CSYF35fx-33E3iVitGcx-OThYRXa5aupj-3RUt-tandIodCwIS0zzddNhNM1a6CHjHaz7ZthwfYyWyz6_LYKwlTSaGCss8gevR_zM7Qyxos4TIolyojuuQmQU2pBJU_-OKZjxz37Ujv3iZCjbpxTEw-D46srBlUhYVqe6GNa5DaOybXxu2cnusB2g9OFkZtEO37/44s/Zoprns6vSCeJTQQgYag-GA/h12/h001.JSdV-6oLdv62G8d5ppmpa_egbUvqP-yLB1lCNHChRrM).


### id695121888
[[2024-03-19]] 16:53
> **Searching the Index** - taking a user’s query, interpreting it and then retrieving the most relevant documents from the index. You can also apply algorithms to score and rank the search results based on relevance.


### id695121890
[[2024-03-19]] 16:53
> DoorDash built the indexing system and the search system into two distinct services. They designed them so that each service could scale independently. This way, the document indexing won’t be affected by a big spike in search traffic and vice-versa.


### id695121905
[[2024-03-19]] 16:53
> The indexer is responsible for taking in documents (*food/restaurant listings for example*), and then converting them into an index that can be easily queried. If you query the index for “chocolate donuts” then you should be able to easily find “Dunkin Donuts”, “Krispy Kreme”, etc.


### id695121903
[[2024-03-19]] 16:53
> DoorDash uses Apache Lucene to handle this process and create the inverted index. The index is then split into smaller index segment files so they can easily be replicated.


### id695121893
[[2024-03-19]] 16:53
> DoorDash’s search engine is designed to be a general-purpose service for all the teams at the company. It’s a multi-tenant service.


### id695121892
[[2024-03-19]] 16:53
> In order to address these concerns, the DoorDash team built their search engine with the concept of *Search Stacks*. These are independent collections of indexing/searching services that are dedicated to one particular use-case (one particular index).


