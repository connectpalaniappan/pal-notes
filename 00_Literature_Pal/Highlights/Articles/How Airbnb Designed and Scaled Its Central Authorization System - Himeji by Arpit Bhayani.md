---
title: How Airbnb Designed and Scaled Its Central Authorization System - Himeji
full Title: How Airbnb Designed and Scaled Its Central Authorization System - Himeji
author: Arpit Bhayani
URL: https://www.youtube.com/watch?v=5FIPtC3xJSQ&list=PLsdq-3Z1EPT27BuTnJ_trF7BsaTpYLqst&index=28
published date: 2022-11-06
category: articles
source: reader
tags: [people/pal,shortlist,medium/articles, author/Arpit_Bhayani, reader/reader, date/2024-06-29, area/reader]
created: 2024-06-29
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Arpit Bhayani]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?v=5FIPtC3xJSQ&list=PLsdq-3Z1EPT27BuTnJ_trF7BsaTpYLqst&index=28)
image_url:: [articles image URL](https://i.ytimg.com/vi/5FIPtC3xJSQ/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-06-29]]
last_highlighted_date:: [[2024-06-29]]
published_date:: [[2022-11-06]]
summary:: Build Your Own Redis / DNS / BitTorrent / SQLite - with CodeCrafters.
Sign up and get 40% off - https://app.codecrafters.io/join?via=arpitbbhayani

System Design for Beginners: https://arpitbhayani.me/sys-design
System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Authorization plays a critical role in ensuring that the platform is not abused. For example, Instagram ensures that if an account is made private, only the people allowed can see the posts from it. Such granular fine-grained access control requires a very robust and flexible authorization system.

In this video, we dive deep into how Airbnb achieves this through its in-house service named Himeji and explore its architecture and key design decisions that ensure robustness, extensibility, availability, and ability to scale to millions of users.

# Arpit's System Design Masterclass

I teach a c...


![rw-book-cover](https://i.ytimg.com/vi/5FIPtC3xJSQ/maxresdefault.jpg)

## Highlights
### id739903865
[[2024-06-29]] 07:39
> granular fine grained Access Control requires an extremely robust and flexible authorization


### id739907259
[[2024-06-29]] 07:40
> checking for authentication is not enough when we need granular access control that defines who can do what on our platform


### id739909943
[[2024-06-29]] 07:42
> monolith now this authorization part is very simple in monolith because it's part of everything is part of the same one code base


### id739912553
[[2024-06-29]] 07:49
> n authorization is modeled as a tuple a tuple that contains three items first is the entity second is the relation third is the principle

- [n] Entity#relation@principal 
   Post:123:comment#write@user:123  * [View Highlight](https://read.readwise.io/read/01j1j0nq3qk5ar2q3vbaf4zr14)


## New highlights added June 29, 2024 at 9:06 AM
### id739913574
[[2024-06-29]] 07:59
> we Leverage is we leverage set theory we leverage transitivity so for example what do we typically say we typically say that a user is able to or a user has right privileges on a particular post or on a particular entity implies that a user can read or write to that right so write itself means read or write and owner means read write and owner privileges

- [n] To save storage space  * [View Highlight](https://read.readwise.io/read/01j1j17bqddna4bzejgv72cc98)


## New highlights added July 1, 2024 at 9:39 AM
### id740691144
[[2024-07-01]] 09:19
> detailed evaluation steps to understand how you write it right but it makes it extremely robust and flexible right


### id740691111
[[2024-07-01]] 09:19
> rchitecture so simple and so fast because what happens is you are just doing a simple key lookups


### id740692811
[[2024-07-01]] 09:27
> you would have a set of nodes that are acting as your cache but now when you have that where should you forward your request to which cache server should you forward your request


### id740692799
[[2024-07-01]] 09:27
> consistent hashing helps you determine data ownership


