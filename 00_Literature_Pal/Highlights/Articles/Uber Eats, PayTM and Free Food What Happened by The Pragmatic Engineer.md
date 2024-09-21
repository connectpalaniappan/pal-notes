---
title: Uber Eats, PayTM and Free Food What Happened?
full Title: Uber Eats, PayTM and Free Food What Happened?
author: The Pragmatic Engineer
URL: https://www.youtube.com/watch?app=desktop&utm_source=blog.quastor.org&utm_medium=newsletter&utm_campaign=lessons-from-big-tech-on-building-resilient-payment-systems&_bhlid=7f3607f2e7e9454e1c81b72a4be62b24267c175d&v=PVzcWBmN2L0&feature=youtu.be
published date: 2022-03-23
category: articles
source: reader
tags: [technology,medium/articles, author/The_Pragmatic_Engineer, reader/reader, date/2024-09-16, area/reader]
created: 2024-09-15
assignedTo: people/pal
priority: P4
work: document
---
author:: [[The Pragmatic Engineer]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?app=desktop&utm_source=blog.quastor.org&utm_medium=newsletter&utm_campaign=lessons-from-big-tech-on-building-resilient-payment-systems&_bhlid=7f3607f2e7e9454e1c81b72a4be62b24267c175d&v=PVzcWBmN2L0&feature=youtu.be)
image_url:: [articles image URL](https://i.ytimg.com/vi/PVzcWBmN2L0/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-09-15]]
last_highlighted_date:: [[2024-09-16]]
published_date:: [[2022-03-23]]
summary:: Uber Eats faced issues with their PayTM payment integration, leading to multiple failed transactions for customers. A new response from PayTM caused confusion, resulting in users being charged multiple times. Ultimately, Uber had to pause the PayTM service to fix the problem and improve communication with their payment provider.


![rw-book-cover](https://i.ytimg.com/vi/PVzcWBmN2L0/maxresdefault.jpg)

## Highlights
### id786210678
[[2024-09-15]] 22:14
> idempotent means that an endpoint behaves the exact same way when you try to repeat a transaction


### id786210958
[[2024-09-15]] 22:17
> if you can you should use http status codes to communicate what is going on is it a success or is it an error


## New highlights added September 15, 2024 at 11:17 PM
### id786212521
[[2024-09-15]] 22:23
> payments feeling open versus failing closed this means what happens when you encounter something unexpected failing close means you shut down as soon as you see a message that you're not expecting or you see an exception or something does not look right you just don't do anything so what this would have meant if we failed closes is we just cancel the transaction

- [n] fail closed: on errors, don’t proceed. Cancel the transaction.  * [View Highlight](https://read.readwise.io/read/01j7wdn86wkhjvvrwjjw1qtsh4)


## New highlights added September 16, 2024 at 1:19 AM
### id786260704
[[2024-09-16]] 00:26
> we shut down the paytm integration uh we use the remote feature flag that we did for for mobile apps


### id786261309
[[2024-09-16]] 00:33
> alert on unknown responses as soon as an unknown response or at least multiple


### id786267039
[[2024-09-16]] 01:02
> a lot better with our payments provider on what breaking changes mean and what they should alert us on and you know breaking changes are a little bit tricky


### id786267476
[[2024-09-16]] 01:04
> api signature is definitely
> a breaking change


### id786267541
[[2024-09-16]] 01:05
> changing an endpoint that kind of behaved item potent for for most of the time like this charging when when you don't have enough balance but now it's behaving differently like the second call and the third call it just returns something different is this a breaking change


### id786267415
[[2024-09-16]] 01:04
> return a new new message which is new semantics that should be a breaking change


### id786267601
[[2024-09-16]] 01:06
> rolling out changes to the api in a stage fashion


### id786267634
[[2024-09-16]] 01:06
> deploying high-risk changes gradually or to certain customers


### id786267953
[[2024-09-16]] 01:09
> making change make changes during business hours to the api and give a heads up a big problem


### id786268048
[[2024-09-16]] 01:10
> internal team within a company deploy on friday by all means obviously have your tests covered
> but just let some of your dependencies know that something is is going out especially when there's a behavior change on your api


