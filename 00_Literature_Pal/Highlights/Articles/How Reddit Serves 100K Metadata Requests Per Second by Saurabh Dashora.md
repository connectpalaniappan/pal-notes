---
title: How Reddit Serves 100K Metadata Requests Per Second
full Title: How Reddit Serves 100K Metadata Requests Per Second
author: Saurabh Dashora
URL: https://newsletter.systemdesigncodex.com/p/how-reddit-serves-100k-metadata-requests
published date: 2024-07-16
category: articles
source: reader
tags: [medium/articles, author/Saurabh_Dashora, reader/reader, date/2024-07-17, area/reader]
created: 2024-07-16
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Saurabh Dashora]]
note:: 
source:: [[reader]]
url:: [articles URL](https://newsletter.systemdesigncodex.com/p/how-reddit-serves-100k-metadata-requests)
image_url:: [articles image URL](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd3d2973c-35eb-4c16-855e-53ecb1d7ec11_2130x1264.png)
category:: [[articles]]
date:: [[2024-07-16]]
last_highlighted_date:: [[2024-07-17]]
published_date:: [[2024-07-16]]
summary:: Reddit is like the front page of the Internet. It hosts billions of posts. And a lot many of these posts contain media content such as images, videos, gifs, and so on. While the media content is often stored in object storage, the metadata is different. For example, if you’ve got a video, you might need to store information such as the thumbnail URL, playback URLs, bitrates, and various resolutions.


![rw-book-cover](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd3d2973c-35eb-4c16-855e-53ecb1d7ec11_2130x1264.png)

## Highlights
### id746987857
[[2024-07-16]] 22:41
> While the media content is often stored in object storage, the metadata needs to be stored elsewhere.


