---
title: It's All a Numbers Game - The Dirty Little Secret of Scalable Systems • Martin Thompson • GOTO 2012
full Title: It's All a Numbers Game - The Dirty Little Secret of Scalable Systems • Martin Thompson • GOTO 2012
author: GOTO Conferences
URL: https://www.youtube.com/watch?v=1KRYH75wgy4&ab_channel=GOTOConferences
published date: 2013-03-20
category: articles
source: reader
tags: [medium/articles, author/GOTO_Conferences, reader/reader, date/2024-03-30, area/reader]
created: 2024-03-30
assignedTo: people/pal
priority: P4
work: document
---
author:: [[GOTO Conferences]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?v=1KRYH75wgy4&ab_channel=GOTOConferences)
image_url:: [articles image URL](https://i.ytimg.com/vi/1KRYH75wgy4/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-03-30]]
last_highlighted_date:: [[2024-03-30]]
published_date:: [[2013-03-20]]
summary:: This presentation was recorded at GOTO Aarhus 2012
http://gotocon.com

Martin Thompson - High-Performance Computing Specialist

ABSTRACT
What does it really mean for a system to scale? How do we know we have built a system that scales to meet the business requirements in a cost effective manner? With ever increasing transaction and data volumes we need to take such questions a lot more seriously. It is now becoming critical for many businesses to focus in on the IT costs per user; otherwise they are not profitable. "Just throw hardware at the problem", is getting tired and just does not wash for many organisations.

https://twitter.com/gotocon
https://www.facebook.com/GOTOConference
http://gotocon.com


![rw-book-cover](https://i.ytimg.com/vi/1KRYH75wgy4/maxresdefault.jpg)

## Highlights
### id700087651
[[2024-03-30]] 12:03
> volume can be units of work transactions amount the data process


### id700087761
[[2024-03-30]] 12:05
> scaling is where whenever you increase your volumes you keep your cost reasonable

- [n] Nice definition of scaling i.e. as you take in more volume, your cost should be reasonable  * [View Highlight](https://read.readwise.io/read/01ht854x1s1r1phczj70jk4rzc)


## New highlights added March 30, 2024 at 5:48 PM
### id700169719
[[2024-03-30]] 16:56
> two things there's
> fixed costs and news variable costs and fixed costs and things that you must sink and it could be like development effort upfront it could be buying kit and putting it in a data center it might be building that data center itself but before you take those jumps you need to work with the business to understand what is the volume you're gonna be dealing with and it's the collaborative effort when we're dealing with this because then you can work out do I go for a variable cost model like do I put this on Amazon ec2 or do I actually build my own data center from scratch if

- [n] Fixed costs are upfront costs and infrastructure costs. Need to amortize. Capital vs operational spend. How well do you know the demand? 
   Can they be on demand? Any bulk discounts? Guaranteeing available resources.  * [View Highlight](https://read.readwise.io/read/01ht8npjvzzw9ypd2m4q0kzqra)


### id700169995
[[2024-03-30]] 17:09
> add another node to your system how many more units of work or transaction

- [n] Add another node, how many more transactions can it handle ? 
   Todo: need to create a sheet for capacity planning  * [View Highlight](https://read.readwise.io/read/01ht8nw2bhawb67vx9rxxpyp60)


### id700180801
[[2024-03-30]] 17:12
> what's important so first up I'm a great believer in that the model for the business would be at the core of what you do and this may seem strange in a scalability talk but I think this is absolutely critical if you're gonna build anything for a business start off with the core model great work through the likes of Eric Evans to me and driven design with alistair cockburn been doing on hexagonal architectures it's all but get the pure application at the center keep it free from all sorts of infrastructure build that and measure
> that on its own can that skill and that work independent of all the other things we wrap around it and you'll probably find that it can and you'll probably find that you can get really good clean code by taking that sort of approach well in the hexagonal architecture approach well how do they then persist that well you provide an adopter that persists it right that's one of the design approaches and not I'm not going to in a detail about how to do that but also our gavin's talks about using
> repository designs for how you persist stuff and not where you can get around a persistence side well how do I get data coming in you're gonna layer things and you're gonna have adopters and channels to bring the data into you so you think let's get the core model together let's test it let's make sure it works correctly it is what the business require I can then feed it with data and then I can see that see if Li I can then work out what all of the characteristics to make that skill but it's important to get that core model correct and don't in
> fact it with infrastructure for how do I see if something how did I do something so I'm probably good for heretic if somebody starts in use an ORM I just run away screaming because you're just mixing concerns at that point and you're gonna really struggle with scaling because you've just limited all of your options if you have a pure clean model and then you have I see a repository pattern that you can choose to store it in somewhere you can then choose to swap the storage however you want to do that and you've got those options and that way you can work and scale your system

- [n] Pure model without any infrastructure 
   Aggregate for clear entry points
   Minimal public interface 
   Clean simple code 
   Later around the core  * [View Highlight](https://read.readwise.io/read/01ht8pkx22a9a5g6dqnx2ahzdn)


## New highlights added March 31, 2024 at 1:04 PM
### id700429898
[[2024-03-31]] 09:45
> I mentioned we need a performance test and profile I think this is absolutely critical how many people here grow on a profiler at least even once a week very very few how do you know your code even does how do you get a feel for what its gonna perform like the understanding it there's a good quote back from one of the Microsoft press I while ago saying
> that if you're gonna develop systems you should all walk through it in a debugger and there's something I took on a fund it was very very valuable write your code right do you so write your test write your code run your tests step through it in a debugger and so amazing the things you see it gives you a whole reinforced picture of the model and how it works same thing happens with a profiler you start to understand the characteristics your system you develop a much better relationship with your system and just understand and get a feel for it but writing good performance

- [n] Component performance test
   System performance test
   Production monitoring
   Common performance mistakes 
   Theory of constraints
   Drives the economics of development  * [View Highlight](https://read.readwise.io/read/01htaff8cgn2bh9eewam6mpt1x)


### id700431144
[[2024-03-31]] 09:49
> I find the performance issues actually in the tests rather than in the target code so how do you address that well first thing do test first development and this really modders is even more for performance test than it does for a normal unit test is you write it against the blank something that just returns straight away with the false answer

- [n] Test driven development for performance tests too  * [View Highlight](https://read.readwise.io/read/01htafs8fe92b6rz47q96etk4s)


### id700431242
[[2024-03-31]] 09:50
> same customer of the same product or the same entity of whatever type over and over

- [n] Never test for the same entity again and again  * [View Highlight](https://read.readwise.io/read/01htafva06kez60md86yfpjdmg)


