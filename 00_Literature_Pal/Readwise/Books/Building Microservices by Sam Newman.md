---
Title: Building Microservices
Full Title: Building Microservices
Author: Sam Newman
Notes: 
URL: 
Published date: 
Category:: books
Source: kindle
Note Created: <% tp.date.now("dddd Do MMMM YYYY HH:mm") %>
Last modified: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm") %>
---
author:: [[Sam Newman]]
note:: 
source:: [[kindle]]
url:: 
image_url:: [books image URL](https://images-na.ssl-images-amazon.com/images/I/51e6hCWFZNL._SL200_.jpg)
category:: [[books]]
date:: [[2024-03-13]]
last_highlighted_date:: [[2019-12-27]]
published_date:: [[]]
summary:: None

![rw-book-cover](https://images-na.ssl-images-amazon.com/images/I/51e6hCWFZNL._SL200_.jpg)

## Highlights
### Location 161
[[2019-12-26]] 22:56
> Robert C. Martin’s definition of the Single Responsibility Principle, which states “Gather together those things that change for the same reason, and separate those things that change for different reasons.”


### Location 184
[[2019-12-26]] 22:56
> communication between the services themselves are via network calls, to enforce separation between the services and avoid the perils of tight coupling.


### Location 187
[[2019-12-26]] 22:56
> there is too much sharing, our consuming services become coupled to our internal representations.


### Location 192
[[2019-12-26]] 22:56
> The golden rule: can you make a change to a service and deploy it by itself without changing anything else?


### Location 205
[[2019-12-26]] 22:56
> perhaps the posts the users make could be stored in a document-oriented data store,


### Location 270
[[2019-12-26]] 22:56
> Web, native application, mobile web, tablet app, or wearable device.


### Location 329
[[2019-12-26]] 22:56
> allow some lifecycle management of the modules, such that they can be deployed into a running process, allowing you to make changes without taking the whole process down.


### Location 412
[[2019-12-26]] 22:56
> our architects need to shift their thinking away from creating the perfect end product, and instead focus on helping create a framework in which the right systems can emerge, and continue to grow as we learn more.


### Location 448
[[2019-12-26]] 22:56
> Netflix, for example, has mostly standardized on Cassandra as a data-store technology.


### Location 544
[[2019-12-26]] 22:56
> For your metrics this might be Graphite, and for your health it might be Nagios.


### Location 581
[[2019-12-26]] 22:56
> Dropwizard and Karyon are two open source, JVM-based microcontainers.


### Location 586
[[2019-12-26]] 22:56
> you might want to mandate the use of circuit breakers. In that case, you might integrate a circuit breaker library like Hystrix.


### Location 588
[[2019-12-26]] 22:56
> Dropwizard’s Metrics


### Location 598
[[2019-12-26]] 22:56
> Netflix mitigates this by using sidecar services, which communicate locally with a JVM that is using the appropriate libraries.


### Location 725
[[2019-12-26]] 22:56
> When services are loosely coupled, a change to one service should not require a change to another.


### Location 729
[[2019-12-26]] 22:56
> loosely coupled service knows as little as it needs to about the services with which it collaborates.


### Location 733
[[2019-12-26]] 22:56
> We want related behavior to sit together, and unrelated behavior to sit elsewhere.


### Location 787
[[2019-12-26]] 22:56
> Once you become very proficient, you may decide to skip the step of keeping the bounded context modeled as a module within a more monolithic system, and jump straight for a separate service.


### Location 804
[[2019-12-26]] 22:56
> Prematurely decomposing a system into microservices can be costly, especially if you are new to the domain. In many ways, having an existing codebase you want to decompose into microservices is much easier than trying to go to microservices from the beginning.


### Location 809
[[2019-12-26]] 22:56
> When you start to think about the bounded contexts that exist in your organization, you should be thinking not in terms of data that is shared, but about the capabilities those contexts provide the rest of the domain.


### Location 974
[[2019-12-26]] 22:56
> how do we handle processes that span service boundaries and may be long running?


### Location 983
[[2019-12-26]] 22:56
> With orchestration, we rely on a central brain to guide and drive the process, much like the conductor in an orchestra. With choreography, we inform each part of the system of its job, and let it work out the details, like dancers all finding their way and reacting to others around them in a ballet.


### Location 1131
[[2019-12-26]] 22:56
> HTTP caching proxies like Varnish and load balancers like mod_proxy,


### Location 1239
[[2019-12-26]] 22:56
> WebSockets,


### Location 1247
[[2019-12-26]] 22:56
> recommend REST in Practice (O’Reilly),


### Location 1265
[[2019-12-26]] 22:56
> keep your middleware dumb, and keep the smarts in the endpoints.


### Location 1267
[[2019-12-26]] 22:56
> ATOM is a REST-compliant specification that defines semantics (among other things) for publishing feeds of resources.


### Location 1304
[[2019-12-26]] 22:56
> Enterprise Integration Patterns


### Location 1319
[[2019-12-26]] 22:56
> Reactive extensions, often shortened to Rx, are a mechanism to compose the results of multiple calls together and run operations on them.


### Location 1345
[[2019-12-26]] 22:56
> don’t violate DRY within a microservice, but be relaxed about violating DRY across all services.


### Location 1422
[[2019-12-26]] 22:56
> implementing a reader able to ignore changes we don’t care about — is what Martin Fowler calls a Tolerant Reader.


### Location 1430
[[2019-12-26]] 22:56
> Postel’s Law (otherwise known as the robustness principle), which states: “Be conservative in what you do, be liberal in what you accept from others.”


### Location 1537
[[2019-12-26]] 22:56
> binary protocol


### Location 1599
[[2019-12-26]] 22:56
> Avoiding the trap of putting too much behavior into any intermediate layers is a tricky balancing act.


### Location 1604
[[2019-12-26]] 22:56
> organizations we work for buy commercial off-the-shelf software (COTS) or make use of software as a service (SaaS)


### Location 1614
[[2019-12-26]] 22:56
> “Build if it is unique to what you do, and can be considered a strategic asset; buy if your use of the tool isn’t that special.”


### Location 1723
[[2019-12-26]] 22:56
> In his book Working Effectively with Legacy Code (Prentice-Hall),


### Location 1748
[[2019-12-26]] 22:56
> tools like Structure 101 allow us to see the dependencies between packages graphically.


### Location 1773
[[2019-12-26]] 22:56
> some new algorithms using a logic programming library in the language Clojure.


### Location 1797
[[2019-12-26]] 22:56
> A great place to start is to use a tool like the freely available SchemaSpy, which can generate graphical representations of the relationships between tables.


### Location 1843
[[2019-12-26]] 22:56
> easier to push out changes to configuration files than alter live database tables.


### Location 1847
[[2019-12-26]] 22:56
> situations I’d try to push for keeping this data in configuration files or directly in code,


### Location 1878
[[2019-12-26]] 22:56
> For a more detailed discussion of the subject, you may want to take a look at Refactoring Databases by Scott J. Ambler and Pramod J. Sadalage (Addison-Wesley).


### Location 3212
[[2019-12-26]] 22:56
> we’ll want to monitor the host itself. CPU, memory — all of these things are useful.


### Location 3217
[[2019-12-26]] 22:56
> monitoring the response time of the service is a good idea.


### Location 3219
[[2019-12-26]] 22:56
> track the number of errors we are reporting.


### Location 3232
[[2019-12-26]] 22:56
> use tools like ssh-multiplexers, which allow us to run the same commands on multiple hosts.


### Location 3252
[[2019-12-26]] 22:56
> downstream systems

- [n] Closer to end user  * [Location 3252](https://readwise.io/to_kindle?action=open&asin=B00T3N7XB4&location=3252)


### Location 3405
[[2019-12-26]] 22:56
> Stephen Few’s excellent book Information Dashboard Design: Displaying Data for At-a-Glance Monitoring


### Location 3420
[[2019-12-26]] 22:56
> Riemann is an event server that allows for fairly advanced aggregation and routing of events and can form part of such a solution.


### Location 3421
[[2019-12-26]] 22:56
> Suro is Netflix’s data pipeline and operates in a similar space. Suro is explicitly used to handle both metrics associated with user behavior, and more operational data like application logs.


