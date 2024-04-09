---
title: A Technical Deep Dive on Event Driven Architectures
full Title: A Technical Deep Dive on Event Driven Architectures
author: Quastor
URL: 
published date: 2024-04-03
category: articles
source: reader
tags: [medium/articles, author/Quastor, reader/reader, date/2024-04-06, area/reader]
created: 2024-04-06
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Quastor]]
note:: 
source:: [[reader]]
url:: 
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article4.6bc1851654a0.png)
category:: [[articles]]
date:: [[2024-04-06]]
last_highlighted_date:: [[2024-04-06]]
published_date:: [[2024-04-03]]
summary:: This text explains Event Driven Architectures (EDAs) and their core components like events, brokers, producers, and consumers. EDAs offer benefits like scalability, extensibility, and decoupling of producers and consumers through event brokers. Relevant technologies for implementing EDAs include Kafka for event streams and RabbitMQ for event queues.


![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article4.6bc1851654a0.png)

## Highlights
### id703229097
[[2024-04-06]] 18:36
> Brief History
> The early internet (Web 1.0) mainly consisted of static websites where the content was read-only. The number of people on the web was also small, so sites that did allow commenting (forums, bulletin boards, etc.) didn’t have to deal with too much data.
> HTTP and the request-response paradigm works well for this. A user sends a request for the web page’s content, the web server processes this request and sends back the data. If you have millions of users, then you can have a server pool with hundreds of servers and distribute user requests between them


### id703229069
[[2024-04-06]] 18:36
> Companies now have to deal with thousands of photos/videos being *uploaded* every minute from around the world. Each upload needs to be analyzed (detect any piracy/pornography), compressed, transcoded and distributed to billions of people around the world


### id703229185
[[2024-04-06]] 18:37
> An easier, more scalable way might be to use an Event Driven Architecture. When the user uploads her video, an event is created. Each of the relevant services will consume the event and complete their task asynchronously.


### id703229191
[[2024-04-06]] 18:37
> The core components of an EDA are
> • Producers
> • Consumers
> • Brokers


### id703229370
[[2024-04-06]] 18:40
> An event is just a type of message that signals a change in state or an action within the system.


### id703229404
[[2024-04-06]] 18:40
> although often used interchangeably, an event and a message are different things. An event is a *type* of message; one that denotes an action or state update. All events are messages but not all messages can be considered events. A message could also just be an acknowledgement, a logging metric, an error message, etc.


### id703229408
[[2024-04-06]] 18:40
> With Event Driven Architectures, events are *immutable*.


### id703229491
[[2024-04-06]] 18:41
> **Event Notification pattern** - The event is a short message that just says state has changed. Downstream consumers will need to query upstream producers to get the relevant data.


### id703229511
[[2024-04-06]] 18:41
> **Event-Carried State Transfer pattern** - The event contains all the state that has changed so downstream consumers can get all the relevant info from the event message itself.


## New highlights added April 7, 2024 at 5:38 PM
### id703326155
[[2024-04-06]] 23:31
> Event Producers
> Event producers/sources are the part of the system that are sending events to the broker.
> The role of the producers involves
> • **Event Creation** - take actions/updates from users/other backend services and create events according to a predefined schema
> • **Serialization** - serialize the event using a format like JSON, Avro, Protobuf, etc.
> • **Transmission** - send the serialized event to the event broker

- [n] Responsibilities of Event producer 
   Content received 
   Content validated
   Event created
   Event serialized
   Event sent to broker  * [View Highlight](https://read.readwise.io/read/01htvd25cqav4m64x2y0dzmt3r)


### id703326128
[[2024-04-06]] 23:28
> Events are usually transmitted in batches to prevent unnecessary network congestion. The producer will aggregate messages until
> • A certain time duration passes
> • A configured threshold of accumulated messages is reached


### id703326356
[[2024-04-06]] 23:32
> broker can be partitioned and split up across multiple machines for fault tolerance and scalability.

- [n] Fault tolerance and scalability, load distribution is an key strategy  * [View Highlight](https://read.readwise.io/read/01htvd6n2rsztmenmatk271fze)


## New highlights added April 8, 2024 at 9:13 AM
### id703995065
[[2024-04-08]] 07:59
> One high level way to categorize event brokers is as event streams or event queues


### id703995069
[[2024-04-08]] 07:59
> Event Stream
> An event stream will store a continuous flow of events and each event can be ingested by *multiple* backend services (consumers). Consumers can re-read events they’ve already consumed and go “back in time” (useful if one of the consumers crashes and needs to rebuild its state).

- [n] Event streams are for multiple consumers  * [View Highlight](https://read.readwise.io/read/01htw8my7ez1tvyym4md6ff3jd)


### id703995079
[[2024-04-08]] 07:59
> In an event stream, you can configure messages to be deleted when
> • A TTL (*time to live*) expires
> • Certain conditions have been met (all consumers have read the message or based on a retention period)
> Examples of event streams include Kafka, AWS Kinesis and more (


### id703995081
[[2024-04-08]] 07:59
> Event Queue
> On the other hand, event queues traditionally have *a single consumer* reading each event from the queue. You *could* have multiple consumers, but they would process different events. A single event can only be processed by a single consumer.


### id703995082
[[2024-04-08]] 07:59
> Once a message is consumed (acknowledged by the consumer), it is removed from the queue.
> Examples include AWS SQS, RabbitMQ and more.


### id703995102
[[2024-04-08]] 07:59
> Event Consumers
> Consumers are the backend services that are ingesting messages from the event broker.
> Each message can be processed by a single consumer or by multiple consumers. For example, youtube could have a video upload service that produces an event whenever someone uploads to youtube.
> That event might have multiple consumers that each process the video like
> • A subtitle service for generating subtitles
> • A transcoding service for converting the video to different screen sizes
> • A copyright service that makes sure it’s not pirated
> If you’re dealing with an event stream (like Kafka) then each consumer will have an offset that tracks which messages they’ve already processed (this [offset](https://link.mail.beehiiv.com/ss/c/u001.LUZYrxblx92g0_IcD8eBHdGIVF1xjRpOieF6VWgLwmOEAItzM3qZlGSnsE5ANc90P7L5MMAjvfoYRTiQyBCDn4doWSSQPx9KoBLjG3pwBTfE_31Htz2kt2roq5gk-Jm3rQO7K6rPfwKOFSgi0yWa5lb9SPqEsQTt3sSQsyQk_nzKcLs0tiZJatHvyCfMjji2Kq-gBgL0OJ5zylgP7Dar6DrIrv5vtcaS6eoUSgG_MG2RHvOBuj2HZ9Dr_Zr7_cViWLIl-p07cHf1N3mjxrAnAQ/457/RC0gboHVQ-elY1HdAeUdSA/h24/h001.l-0YfGCcpO_SaVR7S5S1UgAOqPL7MyNiSQkbCcasG8M) will be tracked by Kafka but can be changed by the consumer if the backend service wants to replay past messages).
> With an event queue (like RabbitMQ) the consumers and the queue will use [ack](https://link.mail.beehiiv.com/ss/c/u001.iOwnnfCBjAhkBYm2nnsew3dU0jjHcV63pLRTp4I4SgMfUGXB5Q-WHPK5vDLw5nbOCUWS2lxfGgdzciJc9BBYEdFodPvLB0CjLVJt6DVrw0zuSmyEuJopCLe5JWuzA42ZPRfOYu-c4MH9qDsufjMu9Lps_eiwhRYc1FxVGoLSQQudrHDBQkehcqi6gd9e1bgV0_l2MNpRamZYrdCXdPL1WzhJIHzUSv-hGBCvB2h0fc0/457/RC0gboHVQ-elY1HdAeUdSA/h25/h001.quEQ3_96eLn0UxKr07R2XQqFUY8Jyrxftock0TtH7lY) (acknowledgement) messages to confirm that an event has been ingested.


