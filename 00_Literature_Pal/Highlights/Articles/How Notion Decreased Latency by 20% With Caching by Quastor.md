---
title: How Notion Decreased Latency by 20% With Caching
full Title: How Notion Decreased Latency by 20% With Caching
author: Quastor
URL: 
published date: 2024-08-03
category: articles
source: reader
tags: [technology,medium/articles, author/Quastor, reader/reader, date/2024-08-03, area/reader]
created: 2024-08-03
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Quastor]]
note:: 
source:: [[reader]]
url:: 
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article3.5c705a01b476.png)
category:: [[articles]]
date:: [[2024-08-03]]
last_highlighted_date:: [[2024-08-03]]
published_date:: [[2024-08-03]]
summary:: Notion improved the speed of its website by 20% by implementing SQLite for client-side caching. This change allowed faster page navigation and resolved issues like database corruption and slow disk reads. The Notion team used a “SharedWorker” setup to manage how data is written to the SQLite database across multiple browser tabs.


![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article3.5c705a01b476.png)

## Highlights
### id753978805
[[2024-08-03]] 17:25
> In 2021, Notion started using a SQLite database for caching data in the windows and macOS apps. This change made initial page loads 50% faster and also sped up navigating between pages by 50%.

- [n] Client side caching would reduce latency  * [View Highlight](https://read.readwise.io/read/01j4d5hb7v110gbjgh17m1gcsc)


### id753979001
[[2024-08-03]] 17:27
> SQLite is a great option when you’re writing an app where the user doesn’t have a stable internet connection. It lets you easily store the user’s data on their device and read/write the data with SQL.


### id753980293
[[2024-08-03]] 17:30
> SQLite has libraries for Java, C++, C, Python, JavaScript, Rust, Go and more.

- [n] SQL lite is great to use for embedded systems, mobile app, desktop app and web app  * [View Highlight](https://read.readwise.io/read/01j4d5rh1vpdnr9s01afrgkaem)


