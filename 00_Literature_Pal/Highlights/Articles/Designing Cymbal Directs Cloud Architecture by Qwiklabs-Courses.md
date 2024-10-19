---
title: Designing Cymbal Direct's Cloud Architecture
full Title: Designing Cymbal Direct's Cloud Architecture
author: Qwiklabs-Courses
URL: https://www.youtube.com/watch?v=fTNpdUXQbY0
image URL: [articles image URL](https://i.ytimg.com/vi/fTNpdUXQbY0/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGCQgQyh_MA8=&rs=AOn4CLCmWCu26opolhMhl_Hw6M_JCArs_A)
published date: 2023-02-24
category: articles
source: reader
tags: [technology,work/documented,medium/articles, author/Qwiklabs-Courses, reader/reader, date/2024-10-15, area/reader]
created: 2024-10-15
assignedTo: people/pal
priority: P4
work: document
---
author:: Qwiklabs-Courses
note:: 
source:: reader
url:: [articles URL](https://www.youtube.com/watch?v=fTNpdUXQbY0)
image_url:: [articles image URL](https://i.ytimg.com/vi/fTNpdUXQbY0/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGCQgQyh_MA8=&rs=AOn4CLCmWCu26opolhMhl_Hw6M_JCArs_A)
category:: articles
date:: 2024-10-15
last_highlighted_date:: 2024-10-15
published_date:: 2023-02-24
summary:: Cymbal Direct is working on designing its cloud architecture to improve scalability and streamline its applications. As a Professional Cloud Architect, you will assess the current environment and define business and technical requirements for migration to Google Cloud. The goal is to create a solution that meets these needs while allowing for future enhancements.


![rw-book-cover](https://i.ytimg.com/vi/fTNpdUXQbY0/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGCQgQyh_MA8=&rs=AOn4CLCmWCu26opolhMhl_Hw6M_JCArs_A)

## Highlights
### id799094480
2024-10-15 15:21
> Let’s start by exploring the breadth of considerations involved in the design of a cloud architecture and the role of the Professional Cloud Architect at Cymbal Direct. As a Professional Cloud Architect, your role involves exploring the different aspects of Cymbal Direct’s existing environment and defining the business and technical requirements for its cloud architecture. These requirements determine how you will design the compute, networking, and storage infrastructure for a solution, how you will plan to migrate the existing environment to the cloud, and what future improvements you will envision.
> Assessment is the process of understanding what the current environment looks like and what the requirements are. After you understand the environment and goals, create a plan to get there. Migrating typically means moving from on-premises to the cloud, but it could be moving to Google Cloud from another cloud. It could also be a bit more abstract and mean migrating from the current architecture, whatever that is, to a new one. After your migration, even if you got everything right, you'll often find areas that you can
> improve. You might even have changes you plan on doing to improve the environment before you migrate. You’ll often want to reduce the number of variables and initially migrate infrastructure without modification (often referred to as a “lift and shift” approach). After ensuring that things are working correctly, you can advance to optimization. In our scenario, Cymbal Direct is having scaling issues in the existing environment.
> They have several projects still on-premises and want to migrate those to Google Cloud. Let’s look at Cymbal Direct’s environment and requirements. As a Professional Cloud Architect at Cymbal Direct, you need to understand what the existing environment looks like. Each element of the existing environment or infrastructure needs to be either replicated or replaced with equivalent or better functionality in your cloud solution. Your choices will be based on the availability of a replacement in Google Cloud and the business
> and technical requirements of a particular migration. Cymbal Direct has three major projects: Delivery by drone, partner and product APIs, and a social media highlighting service. As part of your assessment, you'll talk to the people who manage the existing environment and learn about it. This is a simplified version: Cymba Direct’s delivery by drone project has a website frontend, pilot, and truck management system, all of which run on Kubernetes.
> Positional data for drones and trucks is stored in a MongoDB cluster. Drones are connected to VMs through a stateful connection and stream video through Real-time Messaging Protocol (RMTP) to the pilots, as well as commands from the pilots to the drones. For the purchase and product APIs project, the APIs are built into monolithic apps that were not designed for partner integration. The APIs are running on Ubuntu Linux VMs.
> The social media highlighting app is currently a proof of concept. The application currently runs on a single SuSE Linux VM, uses MySQL and Redis, and is written in Python. Hopefully, some things have already attracted your attention. For example, what could you use as a potential solution for Redis? You could do a simple lift and shift and run a VM with Redis on it. Or maybe you should consider using Memorystore, which is Google’s managed Redis implementation.
> Business requirements are critical because they can determine whether a solution is acceptable. You must pay attention to business requirements when determining which solutions are appropriate. An organization’s business requirements can act as a filter to reduce the number of potential available solutions and help you determine which is the correct one for a given scenario. Cymbal Direct’s management wants to ensure that the company’s applications can easily scale to handle demand so that Cymbal Direct can expand to more test markets.
> Business leaders also want to: Streamline development for application modernization and new features and products. Ensure that developers spend as much time on core business functionality as possible, without having to worry about scalability. Let partners order directly through an API. Get a production version of the social media highlighting service functional, while they ensure that no inappropriate content is distributed. Much like business requirements, technical requirements help you determine which potential
> solutions would be appropriate for your cloud architecture. You determine that Cymbal Direct’s technical requirements are to: Move to managed services wherever possible. Ensure that developers can deploy container-based workloads to testing and production environments in a highly scalable environment. Standardize on containers where possible, but also let existing virtualization infrastructure run without a re-write, so it can be slowly refactored over time.
> Securely allow partner integration. Allow for streaming of IoT data from drones. You’ll often see patterns repeat themselves: business requirements that are very similar to technical requirements, or the opposite. You probably noticed these similarities in Cymbal Direct’s requirements. Let’s explore how you could use these requirements to help inform your decision-making. We’ll focus on just one aspect of Cymbal Direct’s environment: the delivery by drone business. For this project, you need to propose a Google Cloud solution for the website frontend, pilot,
> and truck management systems, all of which run on Kubernetes. For technical requirements you have to: Move to managed services wherever possible. Ensure that developers can deploy container-based workloads to testing and production environments in a highly scalable environment. Standardize on containers where possible. To check your work you can ask, “Does it…” Easily scale to handle additional demand when needed?
> Streamline development? After defining requirements, a critical part of your role as a Professional Cloud Architect at Cymbal Direct is to translate those requirements into solutions. You need to define the compute, network, and storage resources that will meet your requirements. Let’s examine a potential solution. This is not intended to be a complete example, but it includes some of the products and services that could be part of your proposed solution. To begin, your solution has a global https load balancer and runs on Google Kubernetes
> Engine. In a real example, you would probably have more information about the GKE setup. You use separate projects for the website and management components. You could also consider what reference architectures already exist that would support your potential solution. Check your workbook for the complete Potential Solutions table. Cymbal Direct needs to evaluate the potential options the organization could use to implement
> a web frontend that is currently running in their on-premises VMs. As a Cloud Architect you could use a decision flow diagram to evaluate Compute Engine, App Engine, Cloud Run, and Google Kubernetes Engine to see whether they meet the business and technical requirements you have identified. Compute Engine and App Engine fail to meet the “container-based” requirement, so they are eliminated from consideration. Cloud Run and GKE both meet the requirements of being “container-based”, “streamline
> development”, and “scale”, but when considering the last requirement of “managed service”, one choice remains in this example decision tree: Cloud Run. In this example situation, Cloud Run appears to be the best potential solution, but you will still need to check whether there are any limiting factors, such as stateful applications, that are not currently supported in Cloud Run. Cymbal Direct has chosen to use GKE initially because it already runs Kubernetes. However, Cymbal Direct is evaluating Cloud Run for future use, or some of the applications
> that are worth investigating. Often, representing your solution graphically will help you understand it in a different way, which is very useful when you present or explain your solution to stakehol 
[Highlight URL](https://read.readwise.io/read/01ja8xfbvpkdhvkgstf6pxdnj7)


