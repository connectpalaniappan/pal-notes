---
title: Internal Developer Platform vs. Internal Developer Portal What’s Up?
full Title: Internal Developer Platform vs. Internal Developer Portal What’s Up?
author: Luca Galante
URL: https://thenewstack.io/internal-developer-platform-vs-internal-developer-portal-whats-up/
published date: 2024-05-08
category: articles
source: reader
tags: [medium/articles, author/Luca_Galante, reader/reader, date/2024-05-12, area/reader]
created: 2024-05-11
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Luca Galante]]
note:: 
source:: [[reader]]
url:: [articles URL](https://thenewstack.io/internal-developer-platform-vs-internal-developer-portal-whats-up/)
image_url:: [articles image URL](https://cdn.thenewstack.io/media/2024/05/654a9421-scalable-platform-architecture-real-time-data-1024x576.jpg)
category:: [[articles]]
date:: [[2024-05-11]]
last_highlighted_date:: [[2024-05-12]]
published_date:: [[2024-05-08]]
summary:: I’m sure you can very easily guess what everyone has been talking about at tech events such as KubeCon Paris
The post Internal Developer Platform vs. Internal Developer Portal: What’s Up? appeared first on The New Stack.


![rw-book-cover](https://cdn.thenewstack.io/media/2024/05/654a9421-scalable-platform-architecture-real-time-data-1024x576.jpg)

## Highlights
### id718512357
[[2024-05-11]] 20:47
> I’m sure you can very easily guess what everyone has been talking about at tech events such as KubeCon Paris and Google Next 24 recently. Yes, [AI](https://thenewstack.io/ai/) of course. Hard to beat that one this year. But it was very interesting (and exciting) to see so many sessions and conversations covering the second most discussed trend (by miles vs. everything else): [platform engineering](https://thenewstack.io/platform-engineering/).
> Humanitec hosted one of the main platform engineering sessions at Next, together with [Google](https://cloud.google.com/?utm_content=inline+mention) Cloud and Thoughtworks, and we almost couldn’t fit everyone in the room.
> ![](https://cdn.thenewstack.io/media/2024/05/284700d1-google-next-24_idp_humanitec-1024x720.jpg)
> Source: Google
> The volume of conversations about platform engineering keeps multiplying year over year, but crucially, so do the quality and concreteness. At KubeCon Detroit just two years ago, I had to explain to most people what platform engineering was. Last year, everyone was talking about it, but there were still a few enterprise-level examples of [internal developer platform (IDP)](https://humanitec.com/blog/what-is-an-internal-developer-platform) implementations discussed.
> This year there’s been a huge jump in the number of [reference architectures for enterprise-grade IDPs](https://thenewstack.io/build-your-idp-at-light-speed-with-a-platform-reference-architecture/) presented and discussed. One of my favorite presentations was by André Alfter of Bechtle, a leading German IT company, who walked through Bechtle’s [IDP for hybrid high-security setups](https://youtu.be/BqH8byL5SHY?si=KyGrb4QTXbiBYnGj&t=290), complete with the open source workload spec [Score](https://score.dev/) and a [platform orchestrator](https://internaldeveloperplatform.org/platform-orchestrators/).
> This is all great and speaks volumes to the rapidly growing maturity of the platform engineering space. Enterprises that don’t yet have a platform initiative underway (or at least in planning) are seriously risking falling behind their competition — technologically, from a tech employer branding perspective, and also in terms of sheer time to market.
> Yet there’s still confusion in the space. And in a good amount of conversations I had, people were still trying to wrap their heads around the difference between internal developer platforms and internal developer portals. A lot of the perplexity comes from people using the same abbreviation, IDP, for both. But the difference between them is now very clear and established.
> What Is an Internal Developer Platform (the OG)?
> [Platform engineering](https://thenewstack.io/want-to-be-a-tech-company-try-platform-engineering/) is the discipline of binding together the tech and tools in your engineering org into golden paths that abstract complexity away from your application developers, enabling self-service and reducing cognitive load.
> The sum of these golden paths, and what the [platform engineering team](https://thenewstack.io/how-platform-teams-can-align-stakeholders/) builds, is an internal developer platform, the original IDP.
> The Bechtle talk presents one of the latest examples of reference [architectures](https://roadmap.sh/software-design-architecture) for enterprise IDPs that follow what has become a standard since the McKinsey team [presented the concept at PlatformCon23](https://www.youtube.com/watch?v=AimSwK8Mw-U).
> ![](https://cdn.thenewstack.io/media/2024/05/b105acfd-aws-idp-architecture-humanitec-1024x647.png)
> Example reference architecture of an IDP on [sponsor_inline_mention slug="amazon-web-services-aws" ]AWS[/sponsor_inline_mention].
> An IDP that is truly enterprise-ready is composed of five planes:
> 1. **Developer control plane:** This is the primary configuration layer and interaction point for platform users. Components include workload specifications such as Score and a [portal for developers](https://humanitec.com/internal-developer-portal) to interact with.
> 2. **Integration and delivery plane:** This plane is about building and storing the image, creating app and infrastructure configs, and deploying the final state. It usually contains a continuous integration (CI) pipeline, an image registry, a [platform orchestrator](https://humanitec.com/products/platform-orchestrator) and a continuous delivery (CD) system.
> 3. **Resource plane:** This is where the actual infrastructure exists, including clusters, databases, storage or DNS services.
> 4. **Monitoring and logging plane:** This plane provides real-time metrics and logs for apps and infrastructure.
> 5. **Security plane:** This manages secrets and identity to protect sensitive information — e.g., storing, managing and securely retrieving API keys and credentials or secrets.
> At the heart of an enterprise-grade platform is a platform orchestrator, the core configuration engine that reads the abstract request of a developer (e.g., “I need a Postgres”) and matches it to the rules and [golden paths defined by the platform engineering](https://thenewstack.io/humanitec-the-golden-path-to-platform-engineering/) team. This is what enables true developer self-service that follows the highest security and compliance standards. A platform orchestrator is the backend of your IDP, where all the core logic is built in by the platform team.
> What Is an Internal Developer Portal (the Frontend)?
> With this context, it’s straightforward to understand portals (like Backstage) as the frontend to your platform. Gartner defines internal developer portals as “an interface to access the capability of an internal developer platform.”
> ![](https://cdn.thenewstack.io/media/2024/05/28580c60-dev-control-plane-idp_humanitec-1024x254.png)
> Portals are, therefore, based on the user interface (UI), as opposed to APIs, command-line interfaces (CLIs) or code-based interfaces (e.g., [Score](https://humanitec.com/products/score)) in your IDP. They let [developers access a catalog of services](https://thenewstack.io/getting-developer-self-service-right/) and scaffolded templates, and provide them and other stakeholders (e.g., executives) with a layer of visibility on top of the underlying IDP.
> Where Do You Start?
> I hope this helps clarify the difference between internal developer platforms and portals. The next natural question is where should you start. As Aaron Erickson, who built the platform at Salesforce, [explained](https://platformengineering.org/blog/what-to-build-first-the-house-or-the-front-door):
> “Building an internal developer platform is like building a house. You should start from the foundations, the backend, then add walls with doors and windows (the frontend) later. To build a platform by starting with a portal is like building a house by starting with the front door.”
> Portals can be a great interface for your developers to access your platform. But make sure you get the [backend](https://humanitec.com/blog/why-every-internal-developer-platform-needs-a-backend) right first. And start small. Use the [minimum viable platform (MVP) framework](https://humanitec.com/blog/how-to-build-a-minimum-viable-platform-mvp) to move quickly and prove value to all key stakeholders before you scale to roll out a full enterprise-grade IDP.
> The post [Internal Developer Platform vs. Internal Developer Portal: What’s Up?](https://thenewstack.io/internal-developer-platform-vs-internal-developer-portal-whats-up/) appeared first on [The New Stack](https://thenewstack.io).


