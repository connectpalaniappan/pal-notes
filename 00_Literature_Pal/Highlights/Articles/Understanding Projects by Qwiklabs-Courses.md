---
title: Understanding Projects
full Title: Understanding Projects
author: Qwiklabs-Courses
URL: https://www.youtube.com/watch?v=StWq-Gr8bYI
published date: 2023-04-25
category: articles
source: reader
tags: [Technology,medium/articles, author/Qwiklabs-Courses, reader/reader, date/2024-04-30, area/reader]
created: 2024-04-30
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Qwiklabs-Courses]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.youtube.com/watch?v=StWq-Gr8bYI)
image_url:: [articles image URL](https://i.ytimg.com/vi/StWq-Gr8bYI/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGDcgUyh_MA8=&rs=AOn4CLABNj1bP4tNPbXGTgsq3S9cJxhAHA)
category:: [[articles]]
date:: [[2024-04-30]]
last_highlighted_date:: [[2024-04-30]]
published_date:: [[2023-04-25]]
summary:: Projects in Google Cloud are organized within a resource hierarchy that includes resources, projects, folders, and an organization node. Projects are essential for managing Google Cloud services and have unique attributes like project ID, name, and number. The Resource Manager tool helps programmatically manage projects by creating, updating, and deleting them.


![rw-book-cover](https://i.ytimg.com/vi/StWq-Gr8bYI/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGDcgUyh_MA8=&rs=AOn4CLABNj1bP4tNPbXGTgsq3S9cJxhAHA)

## Highlights
### id713420560
[[2024-04-30]] 08:38
> The console is used to access and use resources. Resources are organized in projects. To understand this organization, let’s explore where projects fit in the greater Google Cloud resource hierarchy. This hierarchy is made up of four levels, and starting from the bottom up they are: resources, projects, folders, and an organization node. At the first level are resources. These represent virtual machines, Cloud Storage buckets, tables in BigQuery, or anything else
> in Google Cloud. Resources are organized into projects, which sit on the second level. Projects can be organized into folders, or even subfolders. These sit at the third level. And then at the top level is an organization node, which encompasses all the projects, folders, and resources in your organization. Let’s spend a little more time on the second level of the resource hierarchy, projects.


### id713420642
[[2024-04-30]] 08:39
> Projects are the basis for enabling and using Google Cloud services, like managing APIs, enabling billing, adding and removing collaborators, and enabling other Google services. Each project is a separate compartment, and each resource belongs to exactly one project. Projects can have different owners and users, because they’re billed and managed separately. Each Google Cloud project has three identifying attributes: a project ID, a project name,
> and a project number. * The project ID is a globally unique identifier assigned by Google that cannot be changed–it is immutable–after creation. Project IDs are used in different contexts to inform Google Cloud of the exact project to work with. * The project names, however, are user-created. They don’t have to be unique and they can be changed at any time, so they are not immutable.
> * Google Cloud also assigns each project a unique project number. It’s helpful to know that these Google-generated numbers exist, but we won’t explore them much in this course. They are mainly used internally, by Google Cloud, to keep track of resources. So, how are you expected to manage projects? Google Cloud has the Resource Manager tool, designed to programmatically help you do just that. It’s an API that can gather a list of all the projects associated with an account, create
> new projects, update existing projects, and delete projects. It can even recover projects that were previously deleted and can be accessed through the RPC API and the REST API. The third level of the Google Cloud resource hierarchy is folders. You can use folders to group projects under an organization in a hierarchy. For example, your organization might contain multiple departments, each with its own set of Google Cloud resources.
> Folders let you group these resources on a per-department basis. Folders give teams the ability to delegate administrative rights so that they can work independently. To use folders, you must have an organization node, which is the topmost resource in the Google Cloud hierarchy. Everything else attached to that account goes under this node, which includes projects, folders, and other resources.


