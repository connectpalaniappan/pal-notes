---
title: A Framework For System Design Interviews
full Title: A Framework For System Design Interviews
author: ByteByteGo
URL: https://bytebytego.com/courses/system-design-interview/a-framework-for-system-design-interviews
published date: 
category: articles
source: reader
tags: [medium/articles, author/ByteByteGo, reader/reader, date/2024-05-15, area/reader]
created: 2024-05-14
assignedTo: people/pal
priority: P4
work: document
---
author:: [[ByteByteGo]]
note:: 
source:: [[reader]]
url:: [articles URL](https://bytebytego.com/courses/system-design-interview/a-framework-for-system-design-interviews)
image_url:: [articles image URL](https://bytebytego.com/social.png)
category:: [[articles]]
date:: [[2024-05-14]]
last_highlighted_date:: [[2024-05-15]]
published_date:: [[]]
summary:: System design interviews are crucial for showcasing your problem-solving skills and collaborative abilities. Understanding the requirements, proposing a high-level design, and diving deep into the system components are key steps in acing these interviews. Communicating effectively with the interviewer, asking relevant questions, and seeking feedback are essential throughout the process.


![rw-book-cover](https://bytebytego.com/social.png)

## Highlights
### id719878199
[[2024-05-14]] 20:20
> A good interviewer also looks for red flags. Over-engineering is a real disease of many engineers as they delight in design purity and ignore tradeoffs. They are often unaware of the compounding costs of over-engineered systems, and many companies pay a high price for that ignorance. You certainly do not want to demonstrate this tendency in a system design interview. Other red flags include narrow mindedness, stubbornness, etc.


### id719878416
[[2024-05-14]] 20:21
> In a system design interview, giving out an answer quickly without thinking gives you no bonus points. Answering without a thorough understanding of the requirements is a huge red flag as the interview is not a trivia contest. There is no right answer.


### id719878557
[[2024-05-14]] 20:21
> So, do not jump right in to give a solution. Slow down. Think deeply and ask questions to clarify requirements and assumptions. This is extremely important.


### id719878597
[[2024-05-14]] 20:22
> So, do not be afraid to ask questions.


### id719878595
[[2024-05-14]] 20:22
> When you ask a question, the interviewer either answers your question directly or asks you to make your assumptions.


### id719878624
[[2024-05-14]] 20:22
> If the latter happens, write down your assumptions on the whiteboard or paper.


### id719878646
[[2024-05-14]] 20:22
> What kind of questions to ask? Ask questions to understand the exact requirements. Here is a list of questions to help you get started:
> • What specific features are we going to build?
> • How many users does the product have?
> • How fast does the company anticipate to scale up? What are the anticipated scales in 3 months, 6 months, and a year?
> • What is the company’s technology stack? What existing services you might leverage to simplify the design?


### id719878842
[[2024-05-14]] 20:23
> **Candidate**: Is this a mobile app? Or a web app? Or both? 
> **Interviewer**: Both.
> **Candidate**: What are the most important features for the product? 
> **Interviewer**: Ability to make a post and see friends’ news feed.


### id719878863
[[2024-05-14]] 20:23
> **andidate**: Is the news feed sorted in reverse chronological order or a particular order? The particular order means each post is given a different weight. For instance, posts from your close friends are more important than posts from a group. 
> **Interviewer**: To keep things simple, let us assume the feed is sorted by reverse chronological order.


### id719878902
[[2024-05-14]] 20:24
> **Candidate**: How many friends can a user have? 
> **Interviewer**: 5000
> **Candidate**: What is the traffic volume? 
> **Interviewer**: 10 million daily active users (DAU)
> **Candidate**: Can feed contain images, videos, or just text? 
> **Interviewer**: It can contain media files, including both images and videos.


### id719880260
[[2024-05-14]] 20:29
> • Come up with an initial blueprint for the design. Ask for feedback. Treat your interviewer as a teammate and work together. Many good interviewers love to talk and get involved.
> • Draw box diagrams with key components on the whiteboard or paper. This might include clients (mobile/web), APIs, web servers, data stores, cache, CDN, message queue, etc.
> • Do back-of-the-envelope calculations to evaluate if your blueprint fits the scale constraints. Think out loud. Communicate with your interviewer if back-of-the-envelope is necessary before diving into it.


## New highlights added May 14, 2024 at 10:04 PM
### id719880344
[[2024-05-14]] 20:30
> Should we include API endpoints and database schema here? This depends on the problem. For large design problems like “Design Google search engine”, this is a bit of too low level. For a problem like designing the backend for a multi-player poker game, this is a fair game. Communicate with your interviewer.


### id719890354
[[2024-05-14]] 20:41
> You shall work with the interviewer to identify and prioritize components in the architecture. It is worth stressing that every interview is different.


### id719890351
[[2024-05-14]] 20:41
> Sometimes, the interviewer may give off hints that she likes focusing on high-level design. Sometimes, for a senior candidate interview, the discussion could be on the system performance characteristics, likely focusing on the bottlenecks and resource estimations.


### id719890373
[[2024-05-14]] 20:42
> In most cases, the interviewer may want you to dig into details of some system components.


