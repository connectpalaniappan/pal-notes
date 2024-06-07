---
title: Google Cloud Architecture
full Title: Google Cloud Architecture
author: Qwiklabs-Courses
URL: https://www.youtube.com/watch?v=BmsDjKiP_lA
published date: 2023-04-25
category: articles
source: reader
tags: [medium/articles, author/Qwiklabs-Courses, reader/reader, date/2024-04-30, area/reader]
created: 2024-04-30
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Qwiklabs-Courses]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?v=BmsDjKiP_lA)
image_url:: [articles image URL](https://i.ytimg.com/vi/BmsDjKiP_lA/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGCYgRyh_MA8=&rs=AOn4CLALE_iBRS2tTClxA9WAqKl51_5vRQ)
category:: [[articles]]
date:: [[2024-04-30]]
last_highlighted_date:: [[2024-04-30]]
published_date:: [[2023-04-25]]
summary:: Next, let's focus on Google’s specific offerings in the cloud. You can think of the Google Cloud infrastructure in three layers.


![rw-book-cover](https://i.ytimg.com/vi/BmsDjKiP_lA/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGCYgRyh_MA8=&rs=AOn4CLALE_iBRS2tTClxA9WAqKl51_5vRQ)

## Highlights
### id713306802
[[2024-04-29]] 23:38
> Next, let's focus on Google’s specific offerings in the cloud. You can think of the Google Cloud infrastructure in three layers. * At the base layer is networking and security, which lays the foundation to support all of Google’s infrastructure and applications. * On the next layer sit compute and storage. Google Cloud separates, or decouples, as it’s technically called, compute and storage so they can scale independently based on need. * And on the top layer sit the big data and machine learning products, which enable you
> to perform tasks to ingest, store, process, and deliver business insights, data pipelines, and machine learning models. And thanks to Google Cloud, you can accomplish these tasks without needing to manage and scale the underlying infrastructure. Organizations with growing data needs often require lots of compute power to run big data jobs. And as organizations design for the future, the need for compute power only grows.
> Google offers a range of computing services, which includes: * Compute Engine * Google Kubernetes Engine * App Engine * Cloud Functions * Cloud Run Google Cloud also offers a variety of managed storage options. The list includes: * Cloud Storage * Cloud SQL * Cloud Spanner * Cloud Bigtable, and * Firestore Cloud SQL and Cloud Spanner are relational databases, while Bigtable and Firestore are
> NoSQL databases. And then there’s a robust big data and machine learning product line. This includes: * Cloud Storage * Dataproc * Bigtable * BigQuery * Dataflow * Firestore * Pub/Sub * Looker * Cloud Spanner * AutoML, and * Vertex AI, the unified ML platform
> As we previously mentioned, the Google network is part of the foundation that supports all of Google’s infrastructure and applications. Let’s explore how that’s possible. Google’s network is the largest network of its kind, and Google has invested billions of dollars over the years to build it. This network is designed to give customers the highest possible throughput and lowest possible latencies for their applications by leveraging more than 100 content caching nodes worldwide–locations where high demand content is cached for quicker access–to
> respond to user requests from the location that will provide the quickest response time. Google Cloud’s infrastructure is based in five major geographic locations: North America, South America, Europe, Asia, and Australia. Having multiple service locations is important because choosing where to locate applications affects qualities like availability, durability, and latency, which measures the time a packet
> of information takes to travel from its source to its destination. Each of these locations is divided into several different regions and zones. Regions represent independent geographic areas, and are composed of zones. For example, London, or europe-west2, is a region that currently contains three different zones. A zone is an area where Google Cloud resources are deployed. For example, let’s say you launch a virtual machine using Compute Engine–more about
> Compute Engine in a bit–it will run in the zone that you specify to ensure resource redundancy. Zonal resources operate within a single zone, which means that if a zone becomes unavailable, the resources won’t be available either. Google Cloud lets users specify the geographical locations to run services and resources. In many cases, you can even specify the location on a zonal, regional, or multi-regional level.
> This is useful for bringing applications closer to users around the world, and also for protection in case there are issues with an entire region, say, due to a natural disaster. A few of Google Cloud’s services support placing resources in what we call a multi-region. For example, Cloud Spanner multi-region configurations allow you to replicate the database's data not just in multiple zones, but in multiple zones across multiple regions, as defined by the instance configuration.
> These additional replicas enable you to read data with low latency from multiple locations close to or within the regions in the configuration, like The Netherlands and Belgium. Google Cloud currently supports 103 zones in 34 regions, though this is increasing all the time. The most up to date info can be found at cloud.google.com/about/locations.


