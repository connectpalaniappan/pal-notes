---
title: Cloud vs. Traditional Architecture
full Title: Cloud vs. Traditional Architecture
author: Qwiklabs-Courses
URL: https://www.youtube.com/watch?v=oIhmNJQ52SI
published date: 2023-04-25
category: articles
source: reader
tags: [medium/articles, author/Qwiklabs-Courses, reader/reader, date/2024-04-30, area/reader]
created: 2024-04-29
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Qwiklabs-Courses]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?v=oIhmNJQ52SI)
image_url:: [articles image URL](https://i.ytimg.com/vi/oIhmNJQ52SI/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGDAgTih_MA8=&rs=AOn4CLCa_dHeMIyAQQvGhMlNJ3Uew7InAw)
category:: [[articles]]
date:: [[2024-04-29]]
last_highlighted_date:: [[2024-04-30]]
published_date:: [[2023-04-25]]
summary:: Now that you have a better understanding of what cloud computing is, and the infrastructure that supports it, let’s transition to cloud architecture.


![rw-book-cover](https://i.ytimg.com/vi/oIhmNJQ52SI/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGDAgTih_MA8=&rs=AOn4CLCa_dHeMIyAQQvGhMlNJ3Uew7InAw)

## Highlights
### id713264778
[[2024-04-29]] 22:40
> Now that you have a better understanding of what cloud computing is, and the infrastructure that supports it, let’s transition to cloud architecture. In this section, we’ll explore how the cloud compares to traditional architecture. To understand this, we need to look at some history. The trend toward cloud computing started with a first wave known as colocation. Colocation gave users the financial efficiency of renting physical space, instead of investing in data center real estate.
> Virtualized data centers of today, which is the second wave, share similarities with the private data centers and colocation facilities of decades past. The components of virtualized data centers match the physical building blocks of hosted computing—servers, CPUs, disks, load balancers, and so on—but now they’re virtual devices. With virtualization, enterprises still maintained the infrastructure; it’s still a user-controlled and user-configured environment.
> Several years ago, Google realized that its business couldn’t move fast enough within the confines of the virtualization model. So Google switched to a container-based architecture—a fully automated, elastic third-wave cloud that consists of a combination of automated services and scalable data. Services automatically provision and configure the infrastructure used to run applications. Today, Google Cloud makes this third-wave cloud available to Google customers.
> Google believes that, in the future, every company—regardless of size or industry—will differentiate itself from its competitors through technology. Increasingly, that technology will be in the form of software. Great software is based on high-quality data. This means that every company is, or will eventually become, a data company. The virtual world, which includes Google Cloud’s network, is built on physical infrastructure, and all those racks of humming servers use huge amounts of energy.
> Together, all existing data centers use roughly 2% of the world’s electricity. So, Google works to make data centers run as efficiently as possible. Just like our customers, Google is trying to do the right things for the planet. We understand that Google Cloud customers have environmental goals of their own, and running their workloads in Google Cloud can be a part of meeting them. Therefore, it’s important to note that Google's data centers were the first to achieve ISO
> 14001 certification, which is a standard that maps out a framework for improving resource efficiency and reducing waste. This is Google’s data center in Hamina, Finland. The facility is one of the most advanced and efficient data centers in the Google fleet. Its cooling system, which uses sea water from the Bay of Finland, reduces energy use and is the first of its kind anywhere in the world. In our founding decade, Google became the first major company to be carbon neutral.
> In our second decade, we were the first company to achieve 100% renewable energy. By 2030, we aim to be the first major company to operate carbon free.

- [n] Certainly! Virtualization and container-based deployment are two different approaches to deploying and running applications, each with its own advantages and use cases. Here's a clear explanation of the differences between the two, along with examples.
   **Virtualization**:
   Virtualization involves creating a virtual machine (VM) that emulates a complete physical computing environment, including an operating system, hardware resources (CPU, memory, storage, network interfaces), and other system components. Each virtual machine runs on top of a virtualization layer (hypervisor) that manages the sharing of physical resources among multiple VMs.
   Example:
   Let's say you have a physical server with 32 GB of RAM, a quad-core CPU, and 1 TB of storage. Using virtualization, you can create three virtual machines on this server, each with its own operating system (e.g., one running Windows Server, another running Ubuntu, and a third running CentOS). Each VM is allocated a portion of the physical resources, such as 8 GB of RAM, 2 CPU cores, and 200 GB of storage.
   **Container-based Deployment**:
   In contrast, containers provide an isolated, lightweight environment for running applications without the need for a full virtual operating system. Containers share the host operating system's kernel and only package the application code, libraries, and dependencies required to run the application. This makes containers more lightweight and efficient than virtual machines.
   Example:
   Let's consider the same physical server with 32 GB of RAM, a quad-core CPU, and 1 TB of storage, but this time, you want to deploy multiple applications using containers. You can create multiple containers on the same host operating system (e.g., Ubuntu), each running a different application, such as a web server, a database, and a microservice. Each container is isolated from the others and has access to only the resources it requires, such as a portion of the available CPU and memory.
   **Key Differences**:
   1. **Overhead**: Virtual machines have higher overhead since each VM runs a complete operating system, while containers share the host OS kernel, making them more lightweight and efficient.
   2. **Isolation**: Virtual machines provide stronger isolation between guest operating systems, as they are completely separate from each other and the host. Containers, on the other hand, share the host OS kernel, which can introduce potential security risks if not properly managed.
   3. **Resource Utilization**: Virtual machines typically consume more resources (CPU, memory, storage) since each VM runs a complete operating system. Containers are more lightweight and efficient, allowing for better resource utilization on the host system.
   4. **Portability**: Containers are highly portable and can run consistently across different environments (e.g., development, staging, production) with minimal configuration changes. Virtual machines may require more configuration and setup when moving between environments.
   5. **Startup Time**: Containers generally have faster startup times compared to virtual machines, as they don't need to boot an entire operating system.
   In summary, virtualization provides complete isolation and emulates a complete computing environment, while container-based deployment offers a lightweight, efficient way to package and run applications by sharing the host OS kernel. The choice between the two depends on factors such as the level of isolation required, resource utilization, portability, and the specific use case.  * [View Highlight](https://read.readwise.io/read/01hwph8581sx2mcakhcz846v2a)


