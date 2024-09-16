---
title: Designing Uber's Highly Available Emergency SOS Service - Arpit System Design - YouTube |V|0
full Title: Designing Uber's Highly Available Emergency SOS Service - Arpit System Design - YouTube |V|0
author: youtube.com
URL: https://www.youtube.com/watch?index=23&list=PLsdq-3Z1EPT27BuTnJ_trF7BsaTpYLqst&v=gpzGpPiRoCo
published date: 2022-11-27
category: articles
source: reader
tags: [people/pal,resource/tech,medium/articles, author/youtube_com, reader/reader, date/2024-06-28, area/reader]
created: 2024-06-28
assignedTo: people/pal
priority: P4
work: document
---
author:: [[youtube.com]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?index=23&list=PLsdq-3Z1EPT27BuTnJ_trF7BsaTpYLqst&v=gpzGpPiRoCo)
image_url:: [articles image URL](https://i.ytimg.com/vi/gpzGpPiRoCo/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-06-28]]
last_highlighted_date:: [[2024-06-28]]
published_date:: [[2022-11-27]]
summary:: System Design for Beginners: https://arpitbhayani.me/sys-design
System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

An emergency button in a ride-hailing app like Uber can be life-saving but what happens when you click it? What kind of information does it capture? how does it notify the nearest police station?

In this video, we dive deep into the architecture of Uber's emergency SOS service and look at key design decisions that make it so reliable and highly available.

# Arpit's System Design Masterclass

I teach a course on System Design where you'll learn how to intuitively design scalable systems. The course will help you

 - become a better engineer
 - ace your technical discussions
 - get you acquainted with a massive spectrum of topics ranging from Storage Engines, High-throughput systems, to super-clever algorithms behind them.

I have compre...


![rw-book-cover](https://i.ytimg.com/vi/gpzGpPiRoCo/maxresdefault.jpg)

## Highlights
### id739414343
[[2024-06-27]] 23:30
> information needs to be taken from the client side so for example the current location


### id739414346
[[2024-06-27]] 23:30
> they are they should also be made available on the client side to take quick actions


### id739414424
[[2024-06-27]] 23:31
> SOS button was tapped but after the SOS button is tapped the every single second or every two or basically twice a second the location of the client needs to be continuously sent and monitored on the server right


### id739414549
[[2024-06-27]] 23:31
> an optional SMS is
> compiled and sent to the First Responders because there might be now this is a point that most people don't think of now think about it yo


### id739415490
[[2024-06-27]] 23:34
> someone from the internal support team at Uber needs to be notified like they because they are the one who would be coordinating so they also need to be notified so


### id739415591
[[2024-06-27]] 23:36
> will you just send GPS location to police is that is that easy for them to understand no you would want to make life as simple as you can so which is where what you do is you capture the location but you do reverse Geo codin


## New highlights added June 28, 2024 at 8:47 AM
### id739497734
[[2024-06-28]] 07:39
> the reverse geocoded address right is sent to local police Authority uh it can be used to send SMS to your emergency contacts and whatnot right so this is an important component which would be part of the location microservices right


### id739497813
[[2024-06-28]] 07:39
> source button is pressed the location needs to be continuously sent to their backend server


### id739498131
[[2024-06-28]] 07:41
> rapid SOS is a B2B company that offers SOS Services which means that they expose endpoints on which you send some data in some particular format and they send or they forward this data to the nearest local police Authority

- [n] Leverage third party service where ever possible  * [View Highlight](https://read.readwise.io/read/01j1fdtf6684q4vs1rg4mq146r)


### id739498333
[[2024-06-28]] 07:43
> quickly combine the SMS so that is an important design decision


### id739498392
[[2024-06-28]] 07:44
> you have to send the notifications to internal support emergency contact and Rapid SOS in parallel why because
> you just can't say I'll do all these three one after another


### id739498580
[[2024-06-28]] 07:46
> you are hitting the SS button but the emergency service is down you cannot let that happen so the uptime of this service is extremely important


### id739501013
[[2024-06-28]] 07:55
> Kafka gives you native persistence so you will not lose out on data even if Kafka is done due to any reason or Kafka reboots you to any reason and it and it guarantees at least one's delivery so which means that at least once the message would be delivered to the corresponding consumer this means that it might be possible will for the same
> event two messages are like two times the same event is sent to a consumer but that is fine because it's an emergency situation you cannot have a case where message is not at all delivered right


### id739501025
[[2024-06-28]] 07:55
> Kafka is down we fall back on synchronous API so you send an event to Kafka Kafka sends it or or multiple consumers consume it from Kafka instead of that what if the service the emergency service which is writing to Kafka even in the service itself makes API call to those corresponding things you say there is redundancy yes there is but given the criticality of this service


### id739502626
[[2024-06-28]] 08:05
> synchronously from API Gateway to emergency service emergency service would have its own small database in which it would be stored in that particular information now this database would can be used by our internal support team to see where you are what you are doing what's the emergency and the details around it they might use it


### id739512619
[[2024-06-28]] 08:26
> this location needs to be sent to a location service but apart from that the when you are sending this location to the location service for an ASR situation the location service should respond with a reverse geocoded address now this address becomes extremely important for you to render the template on your mobile phone


### id739513262
[[2024-06-28]] 08:31
> how does this location service continuously update the database with your latest information or is showing the chart on where you have been because it needs to have that trail right you would want to help local police to follow the trail that you took right so which is where every single location that is being sent needs to be captured and stored somewhere so that it is rendered efficiently on the for the help of local police or for internal Looper staff to do the internal investigation

- [n] Smart idea to have split the emergency and location service. Emergency provides a snapshot of incidents. Location service provides the trail of location. Emergency service is write critical and read intensive. Location is write intensive and read critical.  * [View Highlight](https://read.readwise.io/read/01j1fgf01pwf7sha7dcytz3e1d)


### id739514043
[[2024-06-28]] 08:32
> location service whenever user sends the location it would be throwing it into Kafka and then it would be consumed by the emergency service which is updating the location in the database which can be later consumed by your but stuffer can be shared with the local police Authority right so that is what you would do with continuously streaming of location data through Kafka to emergency service


### id739514186
[[2024-06-28]] 08:32
> make call to a notification system because notification system would be notifying to your emergency contacts


### id739514203
[[2024-06-28]] 08:32
> invoking the rapid SOS API now this is where when you are creating an emergency the first thing that it would do is invoke a rapid SOS


## New highlights added June 28, 2024 at 10:58 AM
### id739553851
[[2024-06-28]] 10:39
> why do we need to store it in the database how to support like how to use it to for like how to leverage it for your internal support system

- [n] Why is the database shared between emergency service and support service? Does support even need to be a separate service?  * [View Highlight](https://read.readwise.io/read/01j1fr09r7sb6wd09f4eshyt2k)


### id739554182
[[2024-06-28]] 10:42
> multiple servers of support multiple notifications multiple instances of emergency service we are
> using Kafka which gives us very nice reliability and availability location services multiple instances API Gateway itself is internally skilled we still use a managed API Gateway


### id739554194
[[2024-06-28]] 10:42
> emergency service is down which are not consuming it from Kafka because Kafka provides persistence the data would not be lost when it comes back up it


### id739554247
[[2024-06-28]] 10:43
> f rapid SOS is done we can't do much about it right so that is where but obviously Uber might be having something they're not specified it in their job but they might be having something that the


### id739554230
[[2024-06-28]] 10:43
> Uber internal support staff can directly communicate with few of their uh or can himself or herself dire 911 or 100 to inform that in to inform the local police Authority


