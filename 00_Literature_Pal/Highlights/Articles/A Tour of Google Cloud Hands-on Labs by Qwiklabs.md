---
title: A Tour of Google Cloud Hands-on Labs
full Title: A Tour of Google Cloud Hands-on Labs
author: Qwiklabs
URL: https://www.cloudskillsboost.google/paths/36/course_templates/153/labs/469857
published date: 2023-01-25
category: articles
source: reader
tags: [Technology,medium/articles, author/Qwiklabs, reader/reader, date/2024-04-30, area/reader]
created: 2024-04-30
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Qwiklabs]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.cloudskillsboost.google/paths/36/course_templates/153/labs/469857)
image_url:: [articles image URL](https://www.cloudskillsboost.google/favicon-144.png)
category:: [[articles]]
date:: [[2024-04-30]]
last_highlighted_date:: [[2024-04-30]]
published_date:: [[2023-01-25]]
summary:: Google Cloud offers a variety of services for cloud computing, including storage, data analytics, and networking. The Qwiklabs platform provides hands-on labs and courses to learn Google Cloud skills. You can access labs, track progress, and earn badges to validate your knowledge.


![rw-book-cover](https://www.cloudskillsboost.google/favicon-144.png)

## Highlights
### id713554470
[[2024-04-30]] 15:55
> For the best experience, please visit us on a desktop computer using a link sent by email.
> Read the lab instructions carefully before starting the lab. Labs are timed: You cannot pause them.
> GSP282
> ![](https://cdn.qwiklabs.com/GMOHykaqmlTHiqEeQXTySaMXYPHeIvaqa2qHEzw6Occ%3D)
> Overview
> [Google Cloud](https://cloud.google.com/) is a suite of cloud services hosted on Google's infrastructure. From computing and storage to data analytics, machine learning, and networking, Google Cloud offers a wide variety of services and APIs that can be integrated with any cloud-computing application or project, from personal to enterprise-grade.
> [Google Cloud Skills Boost](https://www.cloudskillsboost.google/) is where you can access Google Cloud’s entire catalog of labs and courses. You can discover learning paths, build in-demand cloud skills, track your activity progress, and validate your knowledge with badges. Qwiklabs is the technology platform the labs and courses sit on. You may see the Qwiklabs name in your Google Cloud learning adventure.
> In this introductory-level lab, you take your first steps with Google Cloud by getting hands-on practice with the [Cloud Console](https://cloud.google.com/cloud-console/)—an in-browser UI that lets you access and manage Google Cloud services. You will identify key features of Google Cloud and also learn about the details of the lab environment.
> If you are new to cloud computing or looking for an overview of Google Cloud and the Qwiklabs platform, you are in the right place. Read on to learn about the specifics of this lab and areas that you will get hands-on practice with.
> What you'll learn
> In this lab, you will learn about the following:
> • The lab platform, and how to identify key features of a lab environment
> • How to access the Cloud console with specific credentials
> • Google Cloud projects, and identify common misconceptions about them
> • How to use the Google Cloud Navigation menu to identify types of Google Cloud services
> • Basic roles, and use the Cloud IAM service to inspect actions available to specific users
> • The API library, and examine its chief features
> Prerequisites
> This is an *introductory-level* lab and the first lab you should take if you're unfamiliar with Google Cloud. If you are already experienced with Cloud console, consider taking one of the following labs:
> If you decide to take one, be sure to **end this lab now**.
> If you have a personal or corporate Google Cloud account or project, sign out of that account. If you stay logged in to your personal/corporate account and run the lab in the same browser, your credentials could get confused, resulting in getting logged out of the lab accidentally.
> If you are using a Pixelbook, run your lab an Incognito window.
> Lab fundamentalsFeatures and components
> Regardless of topic or expertise level, all labs share a common interface. The lab that you're taking should look similar to this:
> ![](https://cdn.qwiklabs.com/Gx5QWak6EsvW0PQURmiMyf10sLtl2AT%2BUSrD04WuCzY%3D)
> **Note:** You are not taking the "Creating a Virtual Machine" lab shown in the image; it is used as an example to highlight common features across labs.
> Read the following lab component definitions, and then locate them in the interface.
> Start Lab (button)
> Clicking this button creates a temporary Google Cloud environment, with all the necessary services and credentials enabled, so you can get hands-on practice with the lab's material. This also starts a countdown timer.
> Credit
> The price of a lab. 1 Credit is *usually* equivalent to 1 US dollar (discounts are available when you purchase credits in bulk). Some introductory-level labs (like this one) are free. The more specialized labs cost more because they involve heavier computing tasks and demand more Google Cloud resources.
> Time
> Specifies the amount of time you have to complete a lab. When you click the Start Lab button, the timer will count down until it reaches 00:00:00. When it does, your temporary Google Cloud environment and resources are deleted. Ample time is given to complete a lab, but make sure you don't work on something else while a lab is running: you risk losing all of your hard work!
> Score
> Many labs include a score. This feature is called "activity tracking" and ensures that you complete specified steps in a lab. To pass a lab with activity tracking, you need to complete all the steps *in order*. Only then will you receive completion credit.
> Paying for a lab
> Some labs are free, but others require you to pay. For those, when you click the Start Lab button, a dialog gives you the choice to launch the lab with an access code or credits. If you don't have either, click **Buy credits** and follow the instructions.
> Reading and following instructions
> This browser tab contains the lab instructions. When you start a lab, the Google Cloud console user interface opens in a new browser tab. You will need to switch between the two browser tabs to read the instructions and then perform the tasks. Depending on your physical computer setup, you could also move the two tabs to separate monitors.
> Test your understanding
> Answer the following multiple choice questions to reinforce your understanding of the concepts we've covered so far.
> Task 1. Accessing the Cloud ConsoleStart the lab
> • Now that you understand the key features and components of a lab, click **Start Lab**.
> It may take a moment for the Google Cloud environment and credentials to spin up. When the timer starts counting down and the Start Lab button changes to a red End Lab button, everything is in place and you're ready to sign in to the Cloud console.
> **Note:** Do not click the **End Lab** button until you have completed all the tasks in the lab. When you click the button, your temporary credentials are invalidated and you won't be able to access the work you've done throughout the lab. You must click this button when you finish; if you do not, you won't be able to take another lab. (The Qwiklabs platform has protections in place to prevent concurrent enrollment.)
> Lab details pane
> Now that your lab instance is up and running, look at the **Lab details** pane on the left. It contains an **Open Google Console** button, credentials (username and password), and a **Project ID** field.
> ![](https://cdn.qwiklabs.com/%2FtHp4GI5VSDyTtdqi3qDFtevuY014F88%2BFow%2FadnRgE%3D)
> **Note:** Your credentials will resemble but not match the image; every lab instance generates new temporary credentials.
> Now examine each of these components.
> Open Google Cloud console
> This button opens the [Cloud console](https://cloud.google.com/cloud-console/): the web console and central development hub for Google Cloud. You will do the majority of your work in Google Cloud from this interface.
> Project ID
> A [Google Cloud project](https://cloud.google.com/docs/overview/#projects) is an organizing entity for your Google Cloud resources. It often contains resources and services; for example, it may hold a pool of virtual machines, a set of databases, and a network that connects them together. Projects also contain settings and permissions, which specify security rules and who has access to what resources.
> A *Project ID* is a unique identifier that is used to link Google Cloud resources and APIs to your specific project. Project IDs are unique across Google Cloud: there can be only one **qwiklabs-gcp-xxx....**, which makes it globally identifiable.
> Username and Password
> These credentials represent an identity in the Cloud Identity and Access Management (Cloud IAM) service. This identity has access permissions (a role or roles) that allow you to work with Google Cloud resources in the project you've been allocated. These credentials are *temporary* and will only work for the access time of the lab. When the timer reaches 00:00:00, you will no longer have access to your Google Cloud project with those credentials.
> Sign in to Google Cloud
> Now that you have a better understanding of the **Lab details** pane, use its contents to sign in to the Cloud console.
> 1. Click **Open Google console**.
> This opens the Google Cloud sign-in page in a new browser tab.
> If 


