---
title: How Netflix Implements Load Shedding
full Title: How Netflix Implements Load Shedding
author: Quastor
URL: 
published date: 2024-05-31
category: articles
source: reader
tags: [technology,medium/articles, author/Quastor, reader/reader, date/2024-06-02, area/reader]
created: 2024-06-02
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Quastor]]
note:: 
source:: [[reader]]
url:: 
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article0.00998d930354.png)
category:: [[articles]]
date:: [[2024-06-02]]
last_highlighted_date:: [[2024-06-02]]
published_date:: [[2024-05-31]]
summary:: Netflix implements load shedding in their API Gateway, Zuul, during high-stress periods to prioritize critical user requests. They categorize requests by priority, implement a load shedding algorithm, and validate assumptions using Chaos Engineering principles. Through this approach, Netflix ensures a smoother streaming experience by shedding low-priority requests when necessary.


![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article0.00998d930354.png)

## Highlights
### id728080504
[[2024-06-02]] 07:40
> It doesn't matter how much time you spend on security audits, penetration testing, encryption or whatever. If your customers are setting weak passwords, then *your business is at risk*.


