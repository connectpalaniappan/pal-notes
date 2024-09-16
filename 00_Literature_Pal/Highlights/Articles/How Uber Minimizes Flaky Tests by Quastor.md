---
title: How Uber Minimizes Flaky Tests
full Title: How Uber Minimizes Flaky Tests
author: Quastor
URL: 
published date: 2024-07-05
category: articles
source: reader
tags: [technology,medium/articles, author/Quastor, reader/reader, date/2024-08-11, area/reader]
created: 2024-08-12
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
date:: [[2024-08-12]]
last_highlighted_date:: [[2024-08-11]]
published_date:: [[2024-07-05]]
summary:: Uber created Testopedia to manage and minimize flaky tests, ensuring their thousands of tests are reliable and performant for each code diff. Testopedia analyzes test statistics, categorizes tests, and uses a sliding window algorithm to identify and treat flaky tests efficiently. Uber's system also allows for critical tests, test switches, and non-blocking modes to handle flaky tests without impacting code test coverage.


![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article0.00998d930354.png)

## Highlights
### id756868508
[[2024-08-11]] 11:44
> percentage-based analyzers that will look at a test’s failure percentage over the last N runs.


