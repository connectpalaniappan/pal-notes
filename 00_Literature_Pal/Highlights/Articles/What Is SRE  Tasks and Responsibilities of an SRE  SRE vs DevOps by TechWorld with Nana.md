---
title: What Is SRE | Tasks and Responsibilities of an SRE | SRE vs DevOps
full Title: What Is SRE | Tasks and Responsibilities of an SRE | SRE vs DevOps
author: TechWorld with Nana
URL: https://www.youtube.com/watch?v=OnK4IKgLl24
published date: 2022-02-08
category: articles
source: reader
tags: [medium/articles, author/TechWorld_with_Nana, reader/reader, date/2024-05-09, area/reader]
created: 2024-05-08
assignedTo: people/pal
priority: P4
work: document
---
author:: [[TechWorld with Nana]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?v=OnK4IKgLl24)
image_url:: [articles image URL](https://i.ytimg.com/vi/OnK4IKgLl24/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-05-08]]
last_highlighted_date:: [[2024-05-09]]
published_date:: [[2022-02-08]]
summary:: Understand what SRE or Site Reliability Engineering is exactly and what are the Tasks and Responsibilities of an SRE | SRE vs DevOps
💚   Check out: "What is DevOps" video                                        ►  https://youtu.be/0yWAtQ6wYNM
🧡   Get notified about new upcoming courses                           ►  https://www.techworld-with-nana.com/course-roadmap
💙   Become a DevOps Engineer - full educational program     ►  https://bit.ly/3ICgXwJ
💛   Follow me on IG for behind-the-scenes-content                  ►  https://bit.ly/2F3LXYJ

#sre #techworldwithnana

►  Thank you Loft for sponsoring this video 🙌🏼
►  Try Loft and get 6 months free with my special link 🎉: https://loft.sh/promotions/2022/nana-sre

SRE is becoming a very popular term in the DevOps and generally the software development world. Probably some of you have already heard about it, but are not sure what it is exactly.
So this video gives a detailed look at what SRE or Site Reliability Engineering really is with the goal to clarify all questio...


![rw-book-cover](https://i.ytimg.com/vi/OnK4IKgLl24/maxresdefault.jpg)

## Highlights
### id717236167
[[2024-05-08]] 22:31
> in this video we're going to talk about sre or site reliability engineering which is becoming a very popular term in the devops and generally the software development world and i'm sure many of you are interested to know what it is exactly so first we will see how sre emerged and why was there even a need for sre then we will see what sre definition is what system reliability means exactly and how sre actually works in practice
> like measuring reliability with slas and so on after which we will go into detail and see exactly what are the tasks and responsibilities of an sre role this will make it clear how the work process of an sre team looks like and what are their daily activities and finally we will talk about how sre compares to devops which is a commonly discussed question nowadays so i recommend that you watch my recent
> devops video first where i explain devops in detail because this will make it definitely easier to understand the topics in this video so let's get started in a traditional software development process we have developers and operations as two separate teams each of them with their own goal while developers want to push out application changes as fast as possible to the end users operations want to keep the application
> stable so they are very careful about each and every change and this causes a conflict of interest between these two rows forcing them to work against each other instead of collaborate and devops was actually introduced to help fix exactly this issue again as you learned in my what is devops video however while devos made release process faster these releases were not as stable as ideally wished by devops principles
> plus in devops team there was no dedicated role or person that actually focused full time on keeping systems reliable and that's how the need for sre and a site reliability engineer as a separate role emerged specifically sre was conceptualized at google by ben traynor a software engineer who was given a task to run a
> small team of other software engineers to do what used to be operations work and according to his own definition sre is what happens when you treat operations as a software problem and stuff it with a bunch of software engineers and at its core sre teams are made up of software engineers who build and implement software to improve the reliability of their systems but this definition is of course too
> vague and high level to really understand how it's implemented in practice so let's break it down and analyze each part of this definition step by step so first of all what is a system that we want to keep reliable or what does a system even mean in this definition well the system is the server's infrastructure the platform so the whole deployment environment where the
> application runs now what exactly is reliability and why is it so important to keep our systems reliable imagine you work with emails daily and your email provider is down once a week or your online banking application is down and not accessible regularly this would be unreliable services you can rely that it's available when you need it on the other hand many popular services like gmail twitter youtube etc
> are rarely inaccessible so these systems are pretty reliable but the thing is users usually do not notice reliability of the system it only becomes visible when something goes wrong and the services are down do you remember the recent outage of facebook instagram and other related services that made huge news what about aws server outages that also affected other
> applications that were hosted on aws of course everybody noticed and knew about it when it happened so the more popular and bigger the product or service and the more used the more impact it will have if the service had an outage which means more their team should worry about its reliability now what are the effects or impact of outages or system unreliability well for most of the services this is a lot of unhappy
> customers and lots of lost revenue like imagine online shop is down on a holiday or online bank is not working because of traffic overload this means lots of lost business because people cannot order anything on that shop so system reliability is very important for business okay so we understood that systems need to be reliable but how do we make a system reliable
> or ask differently what makes system unreliable what affects its reliability well the main cause of system becoming unreliable is when you make changes to your system like change something in the infrastructure the platform where the application is running the application itself and its services and so on and this may cause a disruption and break something in the whole setup well as a solution we can say no changes allowed or limit the amount of changes to keep
> systems reliable but that really limits the business we want to make changes and improvements to our application to make it better and increase its business value and stay competitive etc because if our competitor is bringing out new features we need to keep up and that's the main focus of software developers to make those changes and improvements but on the other hand if the application is not accessible that's also bad for business because you may have awesome features
> but nobody can use it because application is down and it's the operations job to take care of that and make sure the application is accessible this means devs want to release fast and ops want to keep stability so traditionally devs would make a change and ops would analyze with hundreds of checklists and mechanisms to make sure the change would not affect the system and this whole analysis and evaluations slows down the release
> process and that's been the major challenge of the traditional way of software development and that's exactly what devops and sre try to solve so what's the specific solution of sre here well sre tries to automate the process of analyzing and evaluating the effects the change will have on our system reliability automation means no checklists or discussions of operations team whether to release the change or
> not or what threats and risks are involved instead the evaluation is based on automated process and this makes releasing changes fast and safe at the same time now before moving on i want to give a shout out to our sponsor loft loft is actually the first platform for platform engineers it lets teams build a self-service kubernetes platform in days rather than years so how it works is that platform teams usually sit in the
> intersection between sre teams and engineering teams they build self-service systems for the engineering teams to be able to get access to cloud computing resources that usually only sres have access to the goal is a better developer experience and that developers can build more resilient applications and test distributed systems more realistically early on in the development process locked is actually also the creator of
> the cluster which is an open source project for creating virtual kubernetes clusters v-cluster is the first certified kubernetes distribution for virtual clusters and it allows to spin up lightweight clusters inside the namespaces of kubernetes clusters which is a great way for securing multi-tenancy in shared clusters for my followers loft actually provides six months free for their paid subscription
> for the first 500 people so if you want to try it out check out my special link and use my promo code for that and now let's continue with our video now how is that automated evaluation done the way it works is using what's called slas so what is an sla sla is basically how reliable a system is going to be to its end users so how often it's going to be up and how often it's going to be down and it's expressed in percentage a service that
> works all the time is never down has a hundred percent sla now you may be thinking of course any service should be 100 reliable right isn't that a natural goal well not really first of all it's very hard to achieve 100 reliability however there are very few things in the world that actually need a hundred percent sla so for example if your internet


