---
title: Why Zomato Switched From Elasticsearch to ClickHouse
full Title: Why Zomato Switched From Elasticsearch to ClickHouse
author: Quastor
URL: 
published date: 2024-05-23
category: articles
source: reader
tags: [Technology,medium/articles, author/Quastor, reader/reader, date/2024-05-25, area/reader]
created: 2024-06-02
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Quastor]]
note:: 
source:: [[reader]]
url:: 
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article1.be68295a7e40.png)
category:: [[articles]]
date:: [[2024-06-02]]
last_highlighted_date:: [[2024-05-25]]
published_date:: [[2024-05-23]]
summary:: Zomato switched from Elasticsearch to ClickHouse to handle their massive logging infrastructure more efficiently, saving costs and improving performance. ClickHouse's architecture and features allowed Zomato to scale their logging system effectively, achieving faster query response times and significant cost savings compared to their previous setup. The switch to ClickHouse enabled Zomato to handle a large volume of log events per minute and improve system resiliency through efficient monitoring and load shedding mechanisms.


![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article1.be68295a7e40.png)

## Highlights
### id724266217
[[2024-05-25]] 04:32
> Due to the exponential growth in the amount of logs, managing the Elasticsearch clusters became increasingly difficult and costly. They had to over-provision servers to handle variable traffic patterns, which led to rising costs and a poor experience.


### id724267094
[[2024-05-25]] 04:42
> • **Log Collection**- Zomato uses Filebeat to collect logs from docker containers and EC2 instances. These logs are forwarded to Kafka for buffering. Zomato uses custom-built Golang workers to collect these logs from Kafka and send them to ClickHouse (*more on this below*)
> • **Data Storage** - ClickHouse ingests and stores the log data. Zomato used a ClickHouse cluster with 10 M6g.16xlarge AWS EC2 nodes (*this article is from July 2023, so this exact figure has probably changed*).
> • **UI App** - Zomato built a custom dashboard that developers can use to view/filter through the log data. They put a lot of effort into making the dashboard responsive, so it has a First Contentful Paint score of 0.95 seconds and a Largest Contentful Paint score of 1.9 second


### id724267028
[[2024-05-25]] 04:49
> Instead, they wanted to *batch* log messages when inserting them to reduce the overhead on ClickHouse.

- [n] Skip index  * [View Highlight](https://read.readwise.io/read/01hyqj1j5vpf5t05h4kn04v0t2)


### id724267098
[[2024-05-25]] 04:42
> Each batch had a maximum size of 20,000 log entries; this kept the delay between generation of a log message and its insertion into ClickHouse to less than 5 seconds.


### id724267157
[[2024-05-25]] 04:43
> ClickHouse is extremely efficient when searching data by primary key, but queries involving other conditions can be costly (*like any other database*).


### id724267163
[[2024-05-25]] 04:43
> To minimize full table scans, ClickHouse provides “Skip” indexes that enable the database to skip reading significant chunks of data that are guaranteed to have no matching values.


### id724267188
[[2024-05-25]] 04:43
> One example of a skip index is a minmax index. This is where the database will store the minimum/maximum values of a column for every datablock. Then, when you’re querying data based on that specific column, ClickHouse can automatically skip any datablocks that have values that fall outside of the query.


### id724267903
[[2024-05-25]] 04:49
> Another type of skip index relies on Bloom Filters. A Bloom Filter is a probabilistic data structure that tells you with certainty if an element **is not** in the set.


### id724267688
[[2024-05-25]] 04:46
> For monitoring, ClickHouse comes with a lot of embedded instrumentation.


### id724267710
[[2024-05-25]] 04:49
> This let the Zomato team collect metrics via Prometheus and visualize them in Grafana.
> They monitored health metrics like
> • CPU and memory usage
> • Network usage
> • Data insertion/query times
> • How many insertions were getting rejected
> To ensure resiliency, the engineering team implemented load shedding. Under times of stress, they would terminate any queries that consumed excessive resources in order to prioritize lightweight queries. This would ensure system availability to the most users.

- [n] Terminate queries taking a lot of time 
   Metrics monitored: CPU, memory, network, latency, error rate  * [View Highlight](https://read.readwise.io/read/01hyqj9qt2mftkbw1dwmvrsjcz)


### id724267748
[[2024-05-25]] 04:47
> • 99% of queries were answered within 10 seconds
> • Ingestion lag time of less than 5 seconds
> • Over a million dollars per year of cost savings compared to Elasticsearch


