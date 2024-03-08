



|Component|Traditional on Premises IT|Co-location|Hosting|IaaS|CaaS|PaaS|Managed Services|FaaS|SaaS|
| :---    | :---        |    :----:   |    :----:   |    :----:   |    :----:   |    :----:   |    :----:   |    :----:   |    :----:   | 
|Pay|Flat charge|Flat charge|Flat charge|Hourly charge|Hourly charge|Application usage|Hourly charge|Application usage|Subscription|
|Data|USER|USER|USER|USER|USER|USER|USER|USER|VENDOR|
|Application - Infra customization|USER|USER|USER|USER|USER|USER|USER|VENDOR|VENDOR|
|Application - Upgrade/Deployment|USER|USER|USER|USER|USER|USER|VENDOR|VENDOR|VENDOR|
|Application - Scalability|USER|USER|USER|USER|USER|VENDOR|VENDOR|VENDOR|VENDOR|
|Application - Disaster Recovery|USER|USER|USER|USER|USER|VENDOR|VENDOR|VENDOR|VENDOR|
|Application - Capacity Planning|USER|USER|USER|USER|USER|VENDOR|VENDOR|VENDOR|VENDOR|
|Application - Dependencies (Database/Cache)|USER|USER|USER|USER|USER|VENDOR|Not related|Not related|VENDOR|
|Runtime|USER|USER|USER|USER|USER|VENDOR|VENDOR|VENDOR|VENDOR|
|Containers|USER|USER|USER|USER|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|
|Operating system|USER|USER|USER|USER|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|
|Virtualization|USER|USER|USER|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|
|Physical Servers|USER|USER|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|
|Storage|USER|USER|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|
|Networking|USER|USER|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|
|Data center|USER|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|VENDOR|

## Self-Hosted services

## Infrastructure as a service (IaaS)
* IaaS is the hardware that powers it all.
* IAAS provides Virtualization, Servers, Storage and Networking
* Users need to manage the OS and its application.
* Pay for what you allocate
* Example: AWS (EC2), GCP (CE), Microsoft Azure (VM)

## Container as a service (CaaS)
* container-based virtualization in which container engines, orchestration and the underlying compute resources
    * are delivered to users as a service from a cloud provider.
* Example: Google Kubernetes Engine(GKE), AWS (EKS), Azure (AKS) and Pivotal (PKS)

### Platform as a service (PaaS)
* PaaS is the set of tools and services designed to make coding and deploying those applications quick and efficient
* PAAS provides IAAS + Runtime + Middleware + Operating systems
* platform is a managed service
* users provide is the application.
* Pay for what you use
* Example: Google App Engine, CloudFoundry, Heroku, AWS (Beanstalk)

### Function as a service (FaaS)
* “I code my application or service and I don't care where it run..just make sure my user is able to get to it when they try.”
* No visibility into the machines 
  * The machines that are being used to run your applications are shielded from you. 
  * They are not available to you to configure. 
  * In most cases they are created to service the request and disappear after the request is served. 
  * For example: When you run a query on BigQuery you do not know how many machines were used to compute that query and serve the response. 
  * Another example is Cloud Run, when you run an app on Cloud Run, a serverless containerization platform, you just write your code and leave the infrastructure and scale to Google Cloud.
* No server management - you do not have to manage any servers or scale them. 
  * For example: Firestore is a serverless database where you just store the data and don’t have to manage any servers, location or data replication, it’s all handled for you.
* Pay for what your application uses - usually per translation or per request or per usage. 
  * This can vary a bit depending on the service. 
  * For example Cloud Functions are priced according to how long your function runs, 
  * how many times it's invoked and how many resources you provision for the function while Vision API is priced based on per image and per feature you apply on the image.
* Use case:
  * Ideal for background activities as the warm-up time to start a server is very high to handle HTTP requests.
* Example: AWS (Lamda), Google Cloud Function

### Managed Services
* The general idea with fully managed is:
  * “I care how and where my service runs because I have a specific type of service that needs more control over the underlying resources and… my application/team benefits from the extra controls.” 
* Visibility and control of machines - 
  * You can choose the number of machines that are being used to run your application. 
  * For example: When configuring Google Kubernetes Engine you get to create your cluster with specific types and number of nodes, number of pods etc. 
* Managed & automated
  * Fully managed means you don't have to set up any machines, the management, patching, backup are mostly all taken care of for you. 
  * The additional controls let you decide how you want to scale and handle High Availability (HA) and Disaster recovery (DR) situations with easy to set up configs. 
* Pay for machine runtime - You pay for however long you run the machines & other resources that your application uses. 
  * This means even if your application is receiving no traffic but your machine is running, you are paying for it. 
  * For example Compute Engine are priced according to the type of machine, vCPU and memory you use and for how long your machine stays running.
* Use case:
  * Ideal to leverage managed service for caching, database.

## Software as a service (SaaS)
* SaaS applications are designed for end-users, delivered over the web
* SaaS provides Application + Data + PaaS
* User needs to provide data