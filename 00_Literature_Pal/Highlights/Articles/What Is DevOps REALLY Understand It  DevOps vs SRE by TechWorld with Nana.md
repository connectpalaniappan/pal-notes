---
title: What Is DevOps? REALLY Understand It | DevOps vs SRE
full Title: What Is DevOps? REALLY Understand It | DevOps vs SRE
author: TechWorld with Nana
URL: https://www.youtube.com/watch?v=0yWAtQ6wYNM
published date: 2022-01-18
category: articles
source: reader
tags: [Technology,medium/articles, author/TechWorld_with_Nana, reader/reader, date/2024-05-09, area/reader]
created: 2024-05-08
assignedTo: people/pal
priority: P4
work: document
---
author:: [[TechWorld with Nana]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?v=0yWAtQ6wYNM)
image_url:: [articles image URL](https://i.ytimg.com/vi/0yWAtQ6wYNM/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-05-08]]
last_highlighted_date:: [[2024-05-09]]
published_date:: [[2022-01-18]]
summary:: The text discusses DevOps, a concept that focuses on collaboration between developers and operations to streamline the application release process. DevOps involves automating tasks like testing, deployment, and infrastructure configuration to create efficient release cycles. SRE, another concept, complements DevOps by emphasizing system reliability through tools and practices.


![rw-book-cover](https://i.ytimg.com/vi/0yWAtQ6wYNM/maxresdefault.jpg)

## Highlights
### id717181747
[[2024-05-08]] 20:06
> if you know my videos you know that i cover various devops tools and concepts on this channel but to address the main question what exactly is devops and that's what we're going to focus on in this video first we'll see why is devops even needed in the application release process and what are the challenges in this process that devops solves of course we will talk about what devops concept actually is we will also see the devops as a separate role and how it evolved as well as what are the
> tasks and responsibilities of a devops engineer and finally we will briefly talk about sre and how sre fits in the whole devops process well devops is a relatively new concept which has been gaining a lot of popularity and taking over the traditional way of software development devops term itself is so broad and includes so many things that it became difficult to exactly define it and clearly set the boundaries of devops
> compared to other it fields so it's encompassing a lot of things the simplest definition is that devops is an intersection of development and operations but where do boundaries of devops start and end which part of development is not devops or what part of operations is not devops and why was there even a need for something between development and operations development and operations are two main
> components in the whole application release process so let's look in detail at this release process starting from the very beginning whenever we're developing an application we always have the same process of delivering that application to the end users so this is the main goal no matter if you use waterfall or agile or whatever approach at its core you create an application and you want to deliver it to your end users so that they can use
> it so let's say you have a great idea about a cool application you define its functionality or in other words what features it will have you coded you tested and now that you have a tested application you want to actually deploy it on a public server and let users access it for that you build and package your application in some kind of executable form so that it can run you configure the public server with all
> the needed stuff like installing any tools the application needs and deploy your application there you configure firewall rules to allow access to the application on the server and you have launched users can start using it so that's the simplified basis of any application release but that's not the end of the journey while in use you of course have to check in on your application is everything running fine are users experiencing any issues
> maybe there are bugs in the application that you didn't catch when testing also can application handle high user loads etc so after launching it you have to actually make sure that your application is accessible and usable by end users and if there are any issues for users of course you should fix them now that was the initial launch of your application but the application development is not done yet if you see users like your application
> you would want to make it even cooler add new features maybe optimize the performance by getting better servers or making your application faster and so on so you still have a lot of things to do and every time you improve your application either the code itself or the server configuration you want to make this improvement accessible to the end users immediately so after the initial launch you do multiple updates to your application and to keep track of these updates you
> version those changes there are many ways to version changes to the application one common way of versioning is with three numbers one for major changes like you replace the framework you use for coding another one for minor changes like you edit one small feature and one for quick small changes or maybe small bug fixes and you do that over and over again you have an idea of improvement you implement it in code you
> test it build and package it you deploy it and once released you observe it in the production to see whether there are any new improvement possibilities or any issues that need to be fixed right away so this gives you a process of continuous delivery of changes an endless cycle of improvements to your application and devops is about making this process of continuous delivery
> fast and with minimal errors and bugs so with devops improvements get created and delivered to users fast but also those improvements are of high quality and well tested and that is a big challenge quickly delivering high quality code now let's see what are exactly the challenges that teams may face during this process and which devops tries to solve during this whole release process we have roadblocks and frictions that
> slow down the process make it too much effort and allow errors to slip through all the way to production now what are the frictions and roadblocks in the release process first and the most important challenge is miscommunication and lack of collaboration between developers and operations so releasing application has two main parts you code the application you deploy and run the application developers are responsible for coding
> operations are responsible for running the application and between these two there might be a gap of i wrote an application but i can't run it or i'm running the application but i don't know how it works so developers would code without considering where or how the code will be deployed while operations would try to deploy without really understanding what and why they are deploying or how the application even works and this
> would result in miscommunications between these two developers finish coding but the deployment guide for the operations team is not good enough or well documented enough so operations team struggles deploying it so release takes longer or developers finish coding but the feature cannot be deployed because it has a lot of issues so the operations throws it back with improvement suggestions this kind of miscommunication could cause stretching the release periods for days and weeks
> and in complex badly maintained projects maybe even month so between the developer is done with the feature and operation starts deploying it there is no clearly defined automated process of handover it's based on a complex bureaucratic process of what checklists need to be completed and what needs to be documented and who needs to manually approve what for the release and so on so no streamlines or automated processes here apart from miscommunications between
> development and operations in a traditional setup where one team is only responsible for development and other team only for operations these two have seemingly different incentives that make it hard for them to work together developers want to push out new features fast that's their incentive while operations want to make sure those changes don't break anything because operations are incentivized to
> maintain stability in production their main focus is to make sure the application is available doesn't crash doesn't show 500 errors to the users and so on this means that operations need to resist the speed of release and check all the aspects of a new release to make sure it's 100 safe which again slows down the process especially considering that operations don't really understand the code or the application
> so it's even more effort for them to evaluate this new release so for example let's say developers developed a new feature which was released but this feature consumes so much resources in the production environment that the servers got overloaded and the application crashed now operations team needs to fix that so because it's the operations who needs to put out the fires when something like this goes wrong developers may not be as careful as operations about the changes
> they release and again focus on releasing new features as fast as possible without really thinking so much about stability so even though the main common goal of everyone in a company should be to deliver high quality applications to the end users fast in practice the more immediate goals are for eac


