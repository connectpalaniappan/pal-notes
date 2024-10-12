---
title: The Architecture of Grab's Data Layer That Serves Millions of Orders Every Day
full Title: The Architecture of Grab's Data Layer That Serves Millions of Orders Every Day
author: Arpit Bhayani
URL: https://www.youtube.com/watch?v=KeV4erIm47o&list=PLsdq-3Z1EPT27BuTnJ_trF7BsaTpYLqst&index=22
image URL: [articles image URL](https://i.ytimg.com/vi/KeV4erIm47o/maxresdefault.jpg?v=63aee213)
published date: 2022-12-31
category: articles
source: reader
tags: [people/pal,shortlist,medium/articles, author/Arpit_Bhayani, reader/reader, date/2024-10-06, area/reader]
created: 2024-10-05
assignedTo: people/pal
priority: P4
work: document
---
author:: Arpit Bhayani
note:: 
source:: reader
url:: [articles URL](https://www.youtube.com/watch?v=KeV4erIm47o&list=PLsdq-3Z1EPT27BuTnJ_trF7BsaTpYLqst&index=22)
image_url:: [articles image URL](https://i.ytimg.com/vi/KeV4erIm47o/maxresdefault.jpg?v=63aee213)
category:: articles
date:: 2024-10-05
last_highlighted_date:: 2024-10-06
published_date:: 2022-12-31
summary:: Build Your Own Redis / DNS / BitTorrent / SQLite - with CodeCrafters.
Sign up and get 40% off - https://app.codecrafters.io/join?via=arpitbbhayani

System Design for Beginners: https://arpitbhayani.me/sys-design
System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Grab processes millions of Food and Mart orders every single day, and the most critical, but brittle part of the infrastructure is the database. Given how critical orders are to Grab, they have to ensure very high availability of the database while ensuring a very fast query time. So, how do they achieve this?

In this video, we take a look at the high-level architecture of the data layer of Grab's Order Platform and see the practices they follow to ensure high availability, stability, and performance at scale.

# Arpit's System Design Masterclass

I teach a course on System Design where you'...


![rw-book-cover](https://i.ytimg.com/vi/KeV4erIm47o/maxresdefault.jpg?v=63aee213)

## Highlights
### id795137860
2024-10-05 22:16
> so grab processes millions of foods and Mart orders every single day and the most critical but brittle part of the infrastructure is the database given how critical orders are to grab they have to ensure a very high availability of the database while ensuring a very fast query tank so how do they achieve this in this video we take a look at a very high level architecture of the data layer of grabs order platform and see the practices they follow to ensure High
> availability stability and performance at scale but before we move forward I'd like to talk to you about a course on system design that I've been running for over a year and a half now the course is a code based course which means I won't be rambling a solution and it will not be a monologue at all instead a small focused group of 50 to 60 Engineers will be brainstorming the systems and designing it together this way we build a very solid system and learn from each other's experiences the course is enrolled by 800 plus Engineers spending 12 Sports and 12 countries Engineers
> from companies like Google Microsoft GitHub slack Facebook Tesla Yelp Flipkart dream11 and many many many more have taken this course and have some wonderful things to say the course is focused on Building Systems the way they are built in the real world we will be focusing heavily on building the right intuition so that you are ready to build any and every system out there we will be discussing the trade-offs of every single decision we make just like how you do in your team we cover topics
> ranging from Real Time text communication for slack to designing our own toilet balancer to cricbuzzes live text commentary to doing impressions counting at scale in all we would be covering roughly 28 systems and the detailed curriculum split week by week can be found in the course page linked in the description down below so if you are looking to learn system design from the first principles you will love this course I have two offerings for you the first one is the live covert best course and the second one is the recorded offering the Live code base course
> happens once every two months and will go on for eight weeks while the recorded course contains the recordings from one of the past cohorts as is if you are in a hurry and want to learn and want to binge learn system design I would recommend going you for the recorded one otherwise the Live code is where you can participate and discuss the systems and its design life with me and the entire cohort the decision is totally up to you the course details prerequisites testimonials can be found on the course page arpitbani dot me slash masterclass I repeat at with many dot me slash
> masterclass and I would highly recommend you to check that out I've also put the link of this course page in the description down below and I'm looking forward to see you in my next cohort so the first step towards architecting a database layer for any such product any such service any search system like this is to understand the kind of queries that we would fire onto this database right so there are two kinds of queries that we typically fire first is transactional query second are analytical queries now transactional queries are classically basically
> getting something updating something deleting something right so basically get an order create an order delete an order update an order these are transactional queries second are the analytical queries where you might want to get historical orders of a particular user or some statistic around orders let's say grouping orders by a particular attribute right these are analytical queries which can take some time and it's okay right so we would be leveraging that now with respect to grab one very interesting thing that happens is they have to be very good at handling
> spikes because the traffic for a platform like grab would not be uniform it would be spiky nature because let's say there is a dinner time you would see a youth search and specifically around a particular time window you would see a massive influx of searches or maybe there is an event and a lot of people order from food and Mart on grab right so which means that handling Pi uh handling spikes is really important right so then let's talk about design goals now this and again this entire
> thing is taken from gravs engineering blog which I've Linked In the description down below I would highly recommend you to check that out so with respect to grab their design goals were pretty simple and straightforward but really important first one stability now when you are architecting a database layer given how critical database is to any system because if databases on everything is done so given how critical database is the most important part or the most important criteria for a good
> design has to be stability that the system has to be stable enough which means it needs to handle a very high level of query per second that would come in plus it needs to be available because given the database is the one that is storing the order basically creating and getting the order which means that if this database goes down it is loss of Revenue which means that your data layer has to be highly available then with respect to availability you can also sense that hey in case there are
> failure because failures are inevitable in case there are some failures here or there it can have degraded performance impact on your system but it should not lead to a complete outage so it's okay for some fragment to be down but some fragment down should not lead to an complete outage this is really important for your business to survive second design goal is around being cost effective it's really important when a company operates at scale a small slow query or a simple looking slow query
> would increase would shoot your infrastructure cost by a huge margin when you talk in absolute terms which means architecture has to be very cost effective third consistency this is so important like you would not as a user when you're using grab when you create an order when you go to the page to see your historical orders you don't want to array my order is not dead you want strong consistency for transactional but eventual still fast enough but eventual consistency for analytics load so
> because transactional queries are really important because when you are updating an order it needs to update right there and then you cannot just say yeah I will update it with some DeLay So you need strong consistency for transactional queries and eventual consistency for analytics queries now these are design goals now let's see how they architected the data layer considering these things now first step is because there are two types of queries one transactional one analytical what if we create or we use
> two types of database one specializing for transactional side one specializing for analytic side now here a key point to note that these analysis is not gigantic analytics you may not need a data warehouse per se but a query that is good with analytics kind of stuff right we will take a look on the on the kind of tech that they choose so transactional database they are called oltp online transactional processing database and analytical database because this is online which means you need almost right there when you fire the
> query you need immediate response you don't want delayed response so these are o l a p database online analytical processing database so first let's talk let's take a look at oltp database so oltp databases are databases which are meant for transactional purposes which means that they would be the single source of truth no matter what right because that is where your orders would be created updated deleted and whatnot okay now these databases are meant to be
> transactional in nature which means that any interaction coming from the user will be directly going to this database there would not be any asynchronous processing over here so which means they need to be able to sustain a huge amount of load so these databases are specialized to be transactional in nature right and they may not hold all data because it's okay if your h 
[Highlight URL](https://read.readwise.io/read/01j9fx88svstr5mz19tz2j95ce)


