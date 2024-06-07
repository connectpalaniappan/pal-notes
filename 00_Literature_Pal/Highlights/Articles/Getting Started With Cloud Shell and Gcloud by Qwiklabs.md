---
title: Getting Started With Cloud Shell and Gcloud
full Title: Getting Started With Cloud Shell and Gcloud
author: Qwiklabs
URL: https://www.cloudskillsboost.google/paths/36/course_templates/153/labs/469859
published date: 2024-01-26
category: articles
source: reader
tags: [medium/articles, author/Qwiklabs, reader/reader, date/2024-04-30, area/reader]
created: 2024-04-30
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Qwiklabs]]
note:: 
source:: [[reader]]
url:: [articles URL](https://www.cloudskillsboost.google/paths/36/course_templates/153/labs/469859)
image_url:: [articles image URL](https://www.cloudskillsboost.google/favicon-144.png)
category:: [[articles]]
date:: [[2024-04-30]]
last_highlighted_date:: [[2024-04-30]]
published_date:: [[2024-01-26]]
summary:: In this hands-on lab you will learn how to connect to computing resources hosted on Google Cloud Platform, and how to use Cloud Shell and Cloud SDK gcloud commands. For a preview, watch the short video &lt;A HREF="https://youtu.be/ZD1zvEyfpLI"&gt;Get Started with Cloud Shell, GCP Essentials&lt;/A&gt;.


![rw-book-cover](https://www.cloudskillsboost.google/favicon-144.png)

## Highlights
### id713554668
[[2024-04-30]] 15:56
> For the best experience, please visit us on a desktop computer using a link sent by email.
> Read the lab instructions carefully before starting the lab. Labs are timed: You cannot pause them.
> GSP002
> ![](https://cdn.qwiklabs.com/GMOHykaqmlTHiqEeQXTySaMXYPHeIvaqa2qHEzw6Occ%3D)
> Overview
> Cloud Shell provides you with command-line access to computing resources hosted on Google Cloud. Cloud Shell is a Debian-based virtual machine with a persistent 5-GB home directory, which makes it easy for you to manage your Google Cloud projects and resources. The `gcloud` command-line tool and other utilities you need are pre-installed in Cloud Shell, which allows you to get up and running quickly.
> In this hands-on lab, you learn how to connect to computing resources hosted on Google Cloud via Cloud Shell with the `gcloud` tool.
> You are encouraged to type the commands themselves, which reinforces the core concepts. Many labs will include a code block that contains the required commands. You can easily copy and paste the commands from the code block into the appropriate places during the lab.
> What you'll do
> • Practice using `gcloud` commands.
> • Connect to compute services hosted on Google Cloud.
> Prerequisites
> • Familiarity with standard Linux text editors such as `vim`, `emacs`, or `nano`.
> Setup and requirementsBefore you click the Start Lab button
> Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click **Start Lab**, shows how long Google Cloud resources will be made available to you.
> This hands-on lab lets you do the lab activities yourself in a real cloud environment, not in a simulation or demo environment. It does so by giving you new, temporary credentials that you use to sign in and access Google Cloud for the duration of the lab.
> To complete this lab, you need:
> • Access to a standard internet browser (Chrome browser recommended).
> **Note:** Use an Incognito or private browser window to run this lab. This prevents any conflicts between your personal account and the Student account, which may cause extra charges incurred to your personal account.
> • Time to complete the lab---remember, once you start, you cannot pause a lab.
> **Note:** If you already have your own personal Google Cloud account or project, do not use it for this lab to avoid extra charges to your account.
> How to start your lab and sign in to the Google Cloud console
> 1. Click the **Start Lab** button. If you need to pay for the lab, a pop-up opens for you to select your payment method. On the left is the **Lab Details** panel with the following:
> • The **Open Google Cloud console** button
> • Time remaining
> • The temporary credentials that you must use for this lab
> • Other information, if needed, to step through this lab
> 2. Click **Open Google Cloud console** (or right-click and select **Open Link in Incognito Window** if you are running the Chrome browser).
> The lab spins up resources, and then opens another tab that shows the **Sign in** page.
> ***Tip:*** Arrange the tabs in separate windows, side-by-side.
> **Note:** If you see the **Choose an account** dialog, click **Use Another Account**.
> 3. If necessary, copy the **Username** below and paste it into the **Sign in** dialog.
> {{{user_0.username | "Username"}}}
> You can also find the **Username** in the **Lab Details** panel.
> 4. Click **Next**.
> 5. Copy the **Password** below and paste it into the **Welcome** dialog.
> {{{user_0.password | "Password"}}}
> You can also find the **Password** in the **Lab Details** panel.
> 6. Click **Next**.
> **Important:** You must use the credentials the lab provides you. Do not use your Google Cloud account credentials. **Note:** Using your own Google Cloud account for this lab may incur extra charges.
> 7. Click through the subsequent pages:
> • Accept the terms and conditions.
> • Do not add recovery options or two-factor authentication (because this is a temporary account).
> • Do not sign up for free trials.
> After a few moments, the Google Cloud console opens in this tab.
> **Note:** To view a menu with a list of Google Cloud products and services, click the **Navigation menu** at the top-left.
> ![](https://cdn.qwiklabs.com/nUxFb6oRFr435O3t6V7WYJAjeDFcrFb16G9wHWp5BzU%3D)
> Activate Cloud Shell
> Cloud Shell is a virtual machine that is loaded with development tools. It offers a persistent 5GB home directory and runs on the Google Cloud. Cloud Shell provides command-line access to your Google Cloud resources.
> 1. Click **Activate Cloud Shell**
> ![](https://cdn.qwiklabs.com/ep8HmqYGdD%2FkUncAAYpV47OYoHwC8%2Bg0WK%2F8sidHquE%3D)
> at the top of the Google Cloud console.
> When you are connected, you are already authenticated, and the project is set to your **Project_ID**, . The output contains a line that declares the **Project_ID** for this session:
> Your Cloud Platform project in this session is set to {{{project_0.project_id | "PROJECT_ID"}}}
> `gcloud` is the command-line tool for Google Cloud. It comes pre-installed on Cloud Shell and supports tab-completion.
> 2. (Optional) You can list the active account name with this command:
> gcloud auth list
> 3. Click **Authorize**.
> **Output:**
> ACTIVE: * ACCOUNT: {{{user_0.username | "ACCOUNT"}}} To set the active account, run: $ gcloud config set account `ACCOUNT`
> 4. (Optional) You can list the project ID with this command:
> gcloud config list project
> **Output:**
> [core] project = {{{project_0.project_id | "PROJECT_ID"}}} **Note:** For full documentation of `gcloud`, in Google Cloud, refer to [the gcloud CLI overview guide](https://cloud.google.com/sdk/gcloud).
> After Cloud Shell is activated, you can use the command line to invoke the Cloud SDK `gcloud` tool or other tools available on the virtual machine instance. Later in the lab, you will use your `$HOME` directory, which is used in persistent disk storage to store files across projects and between Cloud Shell sessions. Your `$HOME` directory is private to you and cannot be accessed by other users.
> Task 1. Configuring your environment
> In this section, you'll learn about aspects of the development environment that you can adjust.
> Understanding regions and zones
> Certain [Google Compute Engine](https://cloud.google.com/compute/docs/instances) resources live in regions or zones. A region is a specific geographical location where you can run your resources. Each region has one or more zones. For example, the `us-central1` region denotes a region in the Central United States that has zones `us-central1-a`, `us-central1-b`, `us-central1-c`, and `us-central1-f`. The following table shows zones in their respective regions:
> Western US
> Central US
> Eastern US
> Western Europe
> Eastern Asia
> us-west1-a
> us-central1-a
> us-east1-b
> europe-west1-b
> asia-east1-a
> us-west1-b
> us-central1-b
> us-east1-c
> europe-west1c
> asia-east1-b
> -
> us-central1-c
> us-east1-d
> europe-west1-d
> aisia-east1-c
> -
> us-central1-f
> -
> -
> -
> Resources that live in a zone are referred to as *zonal* resources. Virtual machine instances and persistent disks live in a zone. If you want to attach a persistent disk to a virtual machine instance, both resources must be in the same zone. Similarly, if you want to assign a static IP address to an instance, the instance must be in the same region as the static IP address.
> **Note:** Learn more about regions and zones and see a complete list in Google Cloud Compute Engine's [Regions and Zones documentation](https://cloud.google.com/compute/docs/regions-zones/).
> 1. Set the region to
> gcloud config set compute/region {{{project_0.startup_script.project_region | REGION}}}
> 2. To view the project region setting, run the following command:
> gcloud config get-value compute/region
> 3. Set the zone to :
> gcloud config set compute/zone {{{project_0.startup_script.project_zone | ZONE}}}
> 4. To view the project zone setting, run the following command:
> gcloud config get-value compute/zone
> Finding project information
> 1. Copy your project ID to your clipboard 


