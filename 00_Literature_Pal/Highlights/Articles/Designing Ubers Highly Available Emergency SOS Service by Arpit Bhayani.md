---
title: Designing Uber's Highly Available Emergency SOS Service
full Title: Designing Uber's Highly Available Emergency SOS Service
author: Arpit Bhayani
URL: https://www.youtube.com/watch?v=gpzGpPiRoCo&list=PLsdq-3Z1EPT27BuTnJ_trF7BsaTpYLqst&index=25
image URL: [articles image URL](https://i.ytimg.com/vi/gpzGpPiRoCo/maxresdefault.jpg)
published date: 2022-11-27
category: articles
source: reader
tags: [people/pal,shortlist,medium/articles, author/Arpit_Bhayani, reader/reader, date/2024-10-05, area/reader]
created: 2024-10-04
assignedTo: people/pal
priority: P4
work: document
---
author:: Arpit Bhayani
note:: 
source:: reader
url:: [articles URL](https://www.youtube.com/watch?v=gpzGpPiRoCo&list=PLsdq-3Z1EPT27BuTnJ_trF7BsaTpYLqst&index=25)
image_url:: [articles image URL](https://i.ytimg.com/vi/gpzGpPiRoCo/maxresdefault.jpg)
category:: articles
date:: 2024-10-04
last_highlighted_date:: 2024-10-05
published_date:: 2022-11-27
summary:: Build Your Own Redis / DNS / BitTorrent / SQLite - with CodeCrafters.
Sign up and get 40% off - https://app.codecrafters.io/join?via=arpitbbhayani

System Design for Beginners: https://arpitbhayani.me/sys-design
System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

An emergency button in a ride-hailing app like Uber can be life-saving but what happens when you click it? What kind of information does it capture? how does it notify the nearest police station?

In this video, we dive deep into the architecture of Uber's emergency SOS service and look at key design decisions that make it so reliable and highly available.

# Arpit's System Design Masterclass

I teach a course on System Design where you'll learn how to intuitively design scalable systems. The course will help you

 - become a better engineer
 - ace your technical discussions
 - get you acquai...


![rw-book-cover](https://i.ytimg.com/vi/gpzGpPiRoCo/maxresdefault.jpg)

## Highlights
### id794743897
2024-10-04 20:28
> so an emergency button in a ride hailing app like uber can be life-saving but what happens when you click it what kind of information does It capture how does it notify the nearest police station in this video we dive deep into the architecture of Uber's emergency SOS service and look at the key design decisions that make it highly available and reliable but before we move forward I'd like to talk to you about a course on system design that I've been running for over a year and a half now the course is a code based course which means I won't be rambling a solution and
> it will not be a monologue at all instead a small focused group of 50 to 60 Engineers will be brainstorming the systems and designing it together this way we build a very solid system and learn from each other's experiences the course is enrolled by 800 plus engineer spanning 12 codes and 12 countries ingenious from companies like Google Microsoft GitHub slack Facebook Tesla Yelp Flipkart dream11 and many many many more have taken this course and have some wonderful things to say the course is focused on Building Systems the way
> they are built in the real world they will be focusing heavily on building the right intuition so that you are ready to build any and every system out there we will be discussing the trade-offs of every single decision we make just like how you do in your team we cover topics ranging from Real Time text communication for slack to designing our own toilet balance side to cricbuzz's live text commentary to doing impressions counting at scale in all we would be covering roughly 28 systems and the detailed curriculum split week by
> week can be found in the course page linked in the description down below so if you are looking to learn system design from the first principles you will love this course I have two offerings for you the first one is the live cohort based course and the second one is the recorded offering the Live code base course happens once every two months and will go on for 8 weeks while the recorded course contains the recordings from one of the past cohorts as is if you are in a hurry and want to learn and want to binge learn system design I would recommend going you for
> the recorded one otherwise the Live code is where you can participate and discuss the systems and its design life with me and the entire code the decision is totally up to you the course details prerequisites testimonials can be found on the course page arpitbani dot me slash masterclass I repeat at with many dot me slash masterclass and I would highly recommend you to check that out I've also put the link of this course page in the description down below and I'm looking forward to see you in my next cohort so during an emergency every single
> second matters which means that whenever a button is stopped you have to do whatever you can to ensure that very quick actions are taken during such time so first of all we'll take a look at what kind of information should we be capturing when an SOS button is pressed on the app so the critical details that we need to capture could be current location the trip details vehicle details and Driver Rider details right some of this information would be available on the server side why some
> information needs to be taken from the client side so for example the current location where the SOS button was pressed that has to be taken from the client side obviously server would not know it but other details like trip details vehicle details driver Rider details all of that can be they are present on the server side but still they are they should also be made available on the client side to take quick actions will take a look at it second when that SOS button is tapped the most critical thing is that every
> like it's not just that where the SOS button was tapped but after the SOS button is tapped the every single second or every two or basically twice a second the location of the client needs to be continuously sent and monitored on the server right this is extremely important to be done because it's an emergency situation you have to ensure that these devices are explicitly monitored no matter what third an optional SMS is
> compiled and sent to the First Responders because there might be now this is a point that most people don't think of now think about it you might be in an emergency situation where you cannot talk on a phone where if let's say the information is sent but you still need to send this to someone else so which is where it might not always be possible for you to give a call to let's say 911 or 100 in India you cannot do that which is where you may have to rely
> on SMS to do it but will you be typing SMS at that time no so which means that there has to be a way to create SMS from all of the details that we are capturing and sending it to the First Responders and more importantly that when you hit the SOS button and someone from the internal support team at Uber needs to be notified like they because they are the one who would be coordinating so they also need to be notified so that they are coordinating that hey are you
> safe or not what has happened has police reached or what not like all of those things Uber some someone from Uber has to take care of that and by the way whatever we are discussing whatever I'll be going through as part of Architecture is all taken from the Uber's engineering block which I'm linking in the description down below highly recommend you to check that out but we'll still dive deeper into why they have made such decisions now the first key decision is around capturing location obviously when an SOS button is pressed you would
> capture the location but hey what will you do with Latin long because when you capture you get GPS location what will you do with GPS location like will you just send GPS location to police is that is that easy for them to understand no you would want to make life as simple as you can so which is where what you do is you capture the location but you do reverse Geo coding so we typically know that hey from lat long we are sorry from an address we try to gather laptop so where G where reverse geocoding comes in
> is where you use the lat long and try to deduce the address out of it now this is a very popular technique called jio like which is called as reverse geocoding you would have also observed this in Google Maps so in Google Maps when you drag and drop a pin like the map pin at a particular place it tries to reduce the address so when you place it near your home it actually tells you some Road name some area name and some city name
> along with that so this is reverse geocoding now when you have this information when I why is this information important now imagine in during an emergency you are in a very stranded place where you don't know where you actually are so which is where how do you communicate where I am let's say you got a chance to call someone how do you know what to say am I you can't say I met this this this coordinate right so that is where reverse geocoding comes in like this is such an important design decision such an important decent
> decision to ensure that during time of an emergency the life like the overall situation is made simpler for the person in a potential danger right okay so now here which is where the reverse geocoded address right is sent to local police Authority uh it can be used to send SMS to your emergency contacts and whatnot right so this is an important component which would be part of the location microservices right and now while this
> is happening we also know that when source button is pressed the location needs to be continuously sent to their backend server so that Uber's internal staff or some of their services can keep an eye on it now when this information is sent you just don't need to send lat long along with that because it's an emergency you would be sending reverse geocoded information and storing it by the way now this way it's easy for them to coordinate with other people because they don't know light wrong they know in
> this area this street this Lane is having the problem right so this is one of the most critica 
[Highlight URL](https://read.readwise.io/read/01j9d4nhdxvr8answsejpy9m82)


