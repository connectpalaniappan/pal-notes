---
title: Cloud Engineer vs DevOps Engineer - Differences and Overlaps of Tasks and Responsibilities
full Title: Cloud Engineer vs DevOps Engineer - Differences and Overlaps of Tasks and Responsibilities
author: TechWorld with Nana
URL: https://www.youtube.com/watch?v=N1-mhvUghb0
published date: 2023-05-08
category: articles
source: reader
tags: [technology,medium/articles, author/TechWorld_with_Nana, reader/reader, date/2024-05-10, area/reader]
created: 2024-05-10
assignedTo: people/pal
priority: P4
work: document
---
author:: [[TechWorld with Nana]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?v=N1-mhvUghb0)
image_url:: [articles image URL](https://i.ytimg.com/vi/N1-mhvUghb0/maxresdefault.jpg)
category:: [[articles]]
date:: [[2024-05-10]]
last_highlighted_date:: [[2024-05-10]]
published_date:: [[2023-05-08]]
summary:: Cloud Engineers manage cloud infrastructure for companies like AWS, Azure, or Google Cloud. They specialize in configuring services to meet business needs securely. DevOps Engineers focus on automating software release processes and may collaborate with Cloud Engineers for infrastructure management.


![rw-book-cover](https://i.ytimg.com/vi/N1-mhvUghb0/maxresdefault.jpg)

## Highlights
### id717938533
[[2024-05-10]] 13:36
> In this video we're going to talk about two  popular roles in software engineering: "DevOps"   and "Cloud Engineer". Now there is a lot of mix up  of these two roles and many people, many companies   often use them interchangeably. They mix the tasks  and responsibilities of these two very often.   There are for example plenty of job descriptions  for DevOps Cloud Engineer or Cloud DevOps   Engineer, which would naturally make you think  that they are the same role. But then why would   you have two names for the same role? And that's  exactly what I'm going to discuss and clarify  
> in this video. So first of all, let's start by  saying that DevOps in Cloud Engineer are actually   two different roles with different purposes and  objectives. But the reason why people mix them   up and even use them interchangeably is, because  they often have many overlapping responsibilities   and skills and also because for relatively  new roles, companies sometimes have hard time  
> defining the boundaries between roles. Like when  a software developer should program full stack web   application, do operations, monitoring, build the  whole CI/CD pipeline, fix the company's Wi-Fi and   change the light bulbs in the office. So basically  just putting anything and everything on one person   or one job description. So in this video we're  gonna define those boundaries and see what a   Cloud engineer does, what DevOps engineer does,  what are the tasks they both do, so the overlaps   between these roles and what is, that really  differentiates them and draws a clear line between  
> the two. And of course since we are on TechWorld  with Nana channel we're gonna see all of that with   actual practical examples, not just some generic  explanations. But first let me get one thing out   of the way, which is that DevOps engineer was  actually not meant as a separate role originally.   DevOps is a concept and a set of principles and  different engineer roles like software developer,  
> IT operation, server administrator and so on were  supposed to implement those DevOps practices and   principles. So that was the original idea of  DevOps. However the reality now looks different   with hundreds of thousands of DevOps Engineer  jobs, which means it actually evolved into its   own engineering role, which I personally think  makes total sense. If you want to know why and   all the details around it, you can watch my videos  on DevOps engineering specifically where I explain  
> all this with the whole evolution of this role  and so on. Okay now that we've established that   DevOps engineer is its own role, let's compare  the two and let's start with the objectives. DevOps Engineer's main objective is to make the  process of releasing software fast, efficient,   without bugs or issues and they achieve  that by automating this whole process. So  
> instead of manual steps of approving the  release, testing the application changes,   validating that everything works or  making sure the security is configured   etc. So the DevOps engineers automate this whole  process so that it's faster without manual human   interaction points. And I actually have a detailed  video on that if you want to see exactly what   DevOps Engineers tasks and responsibilities are,  which I will also link in this video. But in a  
> nutshell that's an objective of a DevOps Engineer.  On the other hand, the cloud engineer's main   objective is to create and manage infrastructure  on cloud, so that applications that companies   developing can run on it. Now you're probably  thinking create and manage cloud infrastructure   that sounds very vague and not really clear and  specific. So let's start from the very beginning.
> First of all we have hundreds of cloud platforms  which are basically companies who went and bought   a whole bunch of computers, server machines, wired  up the whole thing, configured the networking   etc., built the data centers with all those  machines in different locations and other   companies can now rent those servers for the  fraction of the cost. At least that's how it   started, with a simple use case to be able to  rent a server without having to do the whole  
> infrastructure setup yourself, which is a huge  overhead if you only need just a few servers.   But over time that evolved into something much  more powerful and much more complex. Now we   have Cloud platforms that offer way more than  just compute resources, like renting a server.   You can now get not only your whole infrastructure  on cloud, but also a bunch of services on  
> top of that. Like your application needs  database services, cache storage backup,   maybe you want to run the whole application setup  in a kubernetes cluster, you want to store the   docker images on cloud, build the whole CI/CD  pipeline even and you want to do it in multiple   geographic regions. And when you have hundreds  of employees you also want to manage access to   your cloud resources users and permissions and  so on. In cloud platforms now offer all that  
> through their cloud services and we have tons  of small local cloud platforms with maybe one,   two data centers, who only operate in one country  or region, then we have some larger ones and the   gigantic ones like AWS, Google Cloud, Azure. These  three are currently the biggest cloud platforms,   with AWS being by far the most highly used one.  So now whether you are a small startup or a large   company, you can create your entire setup on  a cloud platform, without having to own any  
> infrastructure and often without having to install  and configure things from scratch, like set up a   Docker image registry or installing a kubernetes  cluster on servers, because this type of things   are often provided as managed ready services for  you to use by those cloud providers. So let's take   AWS as an example. So with AWS you get tons of  services that are already configured on top of the  
> actual underlying physical infrastructure. AWS has  services not only for software development, but   also for machine learning, big data processing,  mobile development. It has many types of storage   services based on speed, size, durability. So  you have literally everything on there. But   not only that, you also have an option to create  and manage your own virtual servers and install   things on that yourself or you can let AWS manage  the underlying infrastructure completely for you,  
> by using their higher level managed services.  Or even the combination of both. So you have   all these options, which is very powerful and it  makes the cloud platforms much more than just a   place where you can rent your infrastructure.  But with so many options and so many services   also comes the complexity, which means, sure, now  you don't have to know how to set up an entire  
> registry and set up database with backups  from scratch or manager storage yourself,   you can use the cloud services directly for those  things. But now you need to learn how to use those   services and integrate them or plug them in into  your applications. And those services are specific   to the cloud platform that provides them. So  you need to learn how to use Kubernetes cluster   service on AWS which is called EKS. Or you have  to learn how to use and manage an image registry  
> on AWS called ECR. If you instead go for Azure or  Google cloud or you move away from AWS to one of   those platforms, now you have to learn how to use  the equivalent service on Azure or Google Cloud,   because they work a little bit differently.  And these platforms provide the same services,   but they work differently and have different  configuration options. So you have to learn   all that specific to the platform. The same way  you need to set up the underlying infrastructure,  
> servers, firewall configuration, proxies for  your application, security within your network,   etc. So you need to learn AWS services,  that allow all this configuration. And when you use those services, you don't just  configure them so that your application runs on   it, everything works and that's it. That's  actually not enough. You need to actua


