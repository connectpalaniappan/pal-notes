---
title: Database Internals - SlateDB With Chris Riccomini
full Title: Database Internals - SlateDB With Chris Riccomini
author: The Geek Narrator
URL: https://www.youtube.com/watch?v=wEAcNoJOBFI
image URL: [articles image URL](https://i.ytimg.com/vi/wEAcNoJOBFI/maxresdefault.jpg)
published date: 2024-10-06
category: articles
source: reader
tags: [medium/articles, author/The_Geek_Narrator, reader/reader, date/2024-10-15, area/reader]
created: 2024-10-14
assignedTo: people/pal
priority: P4
work: document
---
author:: The Geek Narrator
note:: 
source:: reader
url:: [articles URL](https://www.youtube.com/watch?v=wEAcNoJOBFI)
image_url:: [articles image URL](https://i.ytimg.com/vi/wEAcNoJOBFI/maxresdefault.jpg)
category:: articles
date:: 2024-10-14
last_highlighted_date:: 2024-10-15
published_date:: 2024-10-06
summary:: Welcome back to another episode! Today, I have a special guest, Chris Riccomini, joining me to delve into the exciting world of databases. In this episode, we focus on SlateDB, a new and innovative database that's making waves in the tech community. We'll cover a wide range of topics, including the architecture of SlateDB, its internals, design decisions, and some fascinating use cases. Chris, a seasoned software engineer with a background at LinkedIn and WePay, shares his journey and the motivations behind creating SlateDB. 🎙️

Chatpers:
00:00 Introduction to the Topic and Guest
01:58 Chris Riccomini's Background and Experience
04:19 The Genesis of SlateDB
04:54 Understanding SlateDB's Architecture
10:22 The Rise of Object Storage in Databases
13:43 Exploring SlateDB's Features and Trade-offs
32:54 Understanding Latency Trade-offs
34:12 Exploring Storage Formats and Manifest Files
37:25 Caching Strategies and Optimizations in SlateDB
50:21 Consistency Guarantees and Transactionality
52:36 Integration and Resour...


![rw-book-cover](https://i.ytimg.com/vi/wEAcNoJOBFI/maxresdefault.jpg)

## Highlights
### id798747052
2024-10-14 19:29
> welcome everyone to the geek nider podcast I'm your host K Yap and in this episode we delve deep into the world of database internals with our special guest Chris romini we will be exploring slate DB a cutting is cloud native embedded database that's making waves in the tech World in our discussion Chris walks us through his extensive career Journey from his days at LinkedIn and VP to his current projects
> including slate DB we will dive deep into the unique aspects of slate DB's architecture including its use of object storage for replication and durability the importance of compute storage separation and its single writer design principle we will also talk about the intricacies of caching consistency guarantees and how slate DB stands against traditional databases like rocks DB Chris sheds light on use cases like
> streaming serverless functions and durable execution where slate DB can be a GameChanger whether you are a backend engineer a database Enthusiast or just curious about the latest Innovations in database technology this episode promises to be both informative and engaging so tune in and get ready to dive into the future of databases with slate DB hello everyone I'm back with
> another very interesting topic another very interesting database today I have Chris with me and we are going to talk about slate DB which is this new H database and we are going to talk about its architecture its internals design decisions some of the use cases and I'm really excited so welcome Chris thanks a lot for joining me today and let's start with a little bit of introduction great thanks for having me yeah so my name name is Chris ramini and I'm uh a
> software engineer by trade I spent about 15 years or so in Industry most of that time was spent as a backend engineer infrastructure engineer at LinkedIn and then at wee and wee is a sort of a payment processor that got acquired by JP Morgan Chase a few years back during that time as I said a lot of back-end infrastructure stuff I spent a bunch of time working on Hadoop at LinkedIn and then streaming stream processing I worked on their uh software load
> balancer for a while which I guess now would be called a service mesh at wee I worked on our data infrastructure and payments infrastructure primarily and was a a manager and principal engineer there for a while since then I left about gosh almost three years ago now I've been doing a combination of writing investing and yeah that's pretty much it on the writing side I read a book with Demitri your boy who's a ex Twitter engineer called The Missing read me which was really not much to do do with
> backend infrastructure but more just a manual we could give new College grads as they were coming into the workforce after saying the same thing like 20 times and one-on ones I am now working with Martin ketman on the second edition of Designing data intensive applications trying to help them ref refresh that a little bit bring it up to speed and then uh I also write a infrastructure newsletter called materialized view and then I do infrastructure Investing For startup PRC to a and then what I'm here to talk about is slate DB which is the the code
> that I'm sometimes writing and mostly reviewing these days so yeah I'll leave it at that awesome yeah so many things and I'm also looking forward to the book the second edition of data intensive application and I've got access on Ori platform early access to it I looked at the the table of content I'm really excited I'll probably soon get my hands on it and probably read more about it yeah fantastic we're it's a I would say a light refresh mostly what we're
> focusing on is dropping some of the technology that's fallen out of favor and adding some of the technology that's come into favor but structurally it's mostly the same and I I think that's really the the main focus for it so hopefully we'll be able to get that out soon yeah awesome awesome cool let's talk about slate debate so on this podcast I've covered around more than 30 databases many of them are modern many of them are let's say not modern but still very interesting in their specific
> use cases like ranging from transactional databases to analytical stream processing databases and like embeded databases and so on there are so many out there and still we want new databases so why was slate BB created and with this I want to slowly move into also defining what exactly is slate DB sure yeah so I think the main motivation that that sort of
> initially got me excited about slate DB was the idea that you could use object storage to essentially replace a lot of the replication and durability code that you would normally write when building a database I like I said I spent 15 plus years watching this with Kafka watching this with hdfs we built our own sort of Kafkaesque Quorum based right ahead log at weay and in all these systems they were distributed and had to handle
> replication and consistency and make decisions about trade-offs and just to operate it was really complicated and painful and the thought was essentially what if we just use object storage for that and that should theoretically like dramatically simplify the database architecture obviously there are some trade-offs there that we can go into but the when I saw I when I first came across this idea it was at wee and we had built as I said this Quorum based
> replication thing for handling credits and debits essentially the primary source of Truth for our payments and the Ops people reluctantly were running it and it was not easy they were also running Kafka which is not easy and they were running Kafka connect and a bunch of other distributed systems and the risk team at that point one of the principal Engineers that worked on the payments team went off and built a graph database and that was mostly in memory however the persistence at the time was like on dis again standard pattern and
> the Ops people essentially said no you need to store the data in object storage oh that's interesting that makes a lot of sense and again it was the Ops folks that were driving this to simplify the architecture and make it easier to run the second time I came around this idea was uh warp stream I was talking with the founders and just immediately it clicked oh my gosh this is really a brilliant idea when I saw what they were doing again coming off of running distributed systems seeing that you could run essentially a stateless agent and just persist everything in Object
> Store on top of that you could it was friendly to byoc you could persist the data in your own buckets really I think drove the point home and so the thought was let's build a database that's sort of cloud native and simplifies the hard parts of operations quite a bit and I looked around thinking surely this must exist and the closest thing I could find was a rock DB Cloud which is essentially a fork of Rox DB from rocket and they
> store they they essentially forked it and and built a system that stores the data in object storage as well as on local disk and the local dis part is the right ahead log that they keep locally and when I say local disc it could be EBS EFS and in fact I believe they have a pluggable layer that they've added where you can use Kinesis or Kafka as well and when I looked at that I was like yeah that's close but I don't want to run Kinesis or kfka and I I would like my right ahead log to be I would
> say more durable than you could get from EBS and available is really the main thing more available than you could get with a A zonal or Regional e EBS and so that was I think when I decided this should probably exist I think in parallel with that there's like multiple threads to the story but in parallel with that I had been talking with the kafa stream folks especially a responsive they're a streaming company by the way these are all this is somewhat self- serving these are all companies that I've put a little bit of money and I should disclaimer that but I
> was talking with the responsive folks and they need stateful stream processing and for them the latency issue is somewhat less sensitive because it is stream processing so goi 
[Highlight URL](https://read.readwise.io/read/01ja6r6wredpr4dc9tsahym8c5)


