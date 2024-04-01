---
title: Monitoring Distributed Systems
full Title: Monitoring Distributed Systems
author: Rob Ewaschuk
URL: https://readwise.io/reader/document_raw_content/27280116
published date: 2016-08-02
category: articles
source: reader
tags: [medium/articles, author/Rob_Ewaschuk, reader/reader, date/2024-03-29, area/reader]
created: 2024-03-29
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Rob Ewaschuk]]
note:: 
source:: [[reader]]
url:: [articles URL](https://readwise.io/reader/document_raw_content/27280116)
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article0.00998d930354.png)
category:: [[articles]]
date:: [[2024-03-29]]
last_highlighted_date:: [[2024-03-29]]
published_date:: [[2016-08-02]]
summary:: Google's SRE teams have key principles for monitoring and alerting systems, focusing on white-box and black-box monitoring. Monitoring helps analyze trends, build dashboards, and diagnose issues for long-term system health. Keeping monitoring systems simple and effective is crucial for successful alerting and problem resolution.


![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article0.00998d930354.png)

## Highlights
### id699593981
[[2024-03-29]] 07:21
> Monitoring
> Collecting, processing, aggregating, and displaying real-time quantitative data about a system, such as query counts and types, error counts and types, processing times, and server lifetimes.


### id699594025
[[2024-03-29]] 07:21
> White-box monitoring Monitoring based on metrics exposed by the internals of the system, including logs, interfaces like the Java Virtual Machine Profiling Interface, or an HTTP handler that emits internal statistics.


### id699594041
[[2024-03-29]] 07:22
> Black-box monitoring Testing externally visible behavior as a user would see it


### id699594374
[[2024-03-29]] 07:24
> Dashboard An application (usually web-based) that provides a summary view of a service’s core metrics. A dashboard may have filters, selectors, and so on, but is prebuilt to expose the metrics most important to its users. The dashboard might also display team information such as ticket queue length, a list of high-priority bugs, the current on-call engineer for a given area of responsibility, or recent pushes.


### id699594474
[[2024-03-29]] 07:25
> Alert
> A notification intended to be read by a human and that is pushed to a system such as a bug or ticket queue, an email alias, or a pager. Respectively, these alerts are classified as tickets, email alerts,1 and pages.


### id699594529
[[2024-03-29]] 07:25
> Root cause
> A defect in a software or human system that, if repaired, instills confidence that this event won’t happen again in the same way. A given incident might have multiple root causes: for example, perhaps it was caused by a combination of insufficient process automation, software that crashed on bogus input, and insufficient testing of the script used to generate the configuration. Each of these factors might stand alone as a root cause, and each should be repaired.


### id699595205
[[2024-03-29]] 07:27
> Node (or machine) Used interchangeably to indicate a single instance of a running kernel in either a physical server, virtual machine, or container. There might be multiple services worth monitoring on a single machine. The services may either be: • Related to each other: for example, a caching server and a web server
> • Unrelated services sharing hardware: for example, a code repository and a master for a configuration system like Puppet or Chef


### id699594445
[[2024-03-29]] 07:25
> Push Any change to a service’s running software or its configuration.


## New highlights added March 29, 2024 at 7:04 PM
### id699749234
[[2024-03-29]] 15:27
> Analyzing long-term trends How big is my database and how fast is it growing? How quickly is my daily-active user count growing?
> Comparing over time or experiment groups Are queries faster with Acme Bucket of Bytes 2.72 versus Ajax DB 3.14? How much better is my memcache hit rate with an extra node? Is my site slower than it was last week?
> Alerting
> Something is broken, and somebody needs to fix it right now! Or, something might break soon, so somebody should look soon.
> Building dashboards
> Dashboards should answer basic questions about your service, and normally include some form of the four golden signals (discussed in “The Four Golden Signals” on page 6).
> Conducting ad hoc retrospective analysis (i.e., debugging) Our latency just shot up; what else happened around the same time?


### id699749471
[[2024-03-29]] 15:29
> Monitoring and alerting enables a system to tell us when it’s broken, or perhaps to tell us what’s about to break


### id699750403
[[2024-03-29]] 15:31
> . When the system isn’t able to automatically fix itself, we want a human to investigate the alert, determine if there’s a real problem at hand, mitigate the problem, and determine the root cause of the problem. Unless you’re performing security auditing on very narrowly scoped components of a system, you should never trigger an alert simply because “something seems a bit weird.”


### id699750425
[[2024-03-29]] 15:31
> Effective alerting systems have good signal and very low noise


### id699751293
[[2024-03-29]] 15:36
> We avoid “magic” systems that try to learn thresholds or automatically detect causality

- [n] Why should magic systems that predict causes need to be avoided 🤔?  * [View Highlight](https://read.readwise.io/read/01ht5yrda9na8j6bsm2r3w64b3)


### id699753400
[[2024-03-29]] 15:40
> Observational experiments conducted over a very long time horizon (months or years) with a low sampling rate (hours or days) can also often tolerate more fragility because occasional missed samples won’t hide a long-running trend


### id699753436
[[2024-03-29]] 15:41
> Dependency-reliant rules usually per4 | Monitoring Distributed Systems


### id699753438
[[2024-03-29]] 15:41
> tain to very stable parts of our system, such as our system for draining user traffic away from a datacenter. For example, “If a datacenter is drained, then don’t alert me on its latency” is one common datacenter alerting rule


### id699753992
[[2024-03-29]] 15:43
> The “what’s broken” indicates the symptom; the “why” indicates a (possibly intermediate) cause.


### id699755822
[[2024-03-29]] 15:50
> black-box monitoring is symptom-oriented and represents active— not predicted—problems: “The system isn’t working correctly, right now.”


### id699755142
[[2024-03-29]] 15:47
> White-box monitoring depends on the ability to inspect the innards of the system, such as logs or HTTP endpoints, with instrumentation


### id699755451
[[2024-03-29]] 15:49
> that in a multilayered system, one person’s symptom is another person’s cause. For example, suppose that a database’s performance is slow. Slow database reads are a symptom for the database SRE who detects them. However, for the frontend SRE observing a slow website, the same slow database reads are a cause. Therefore, whitebox monitoring is sometimes symptom-oriented, and sometimes cause-oriented, depending on just how informative your white-box is.


### id699755994
[[2024-03-29]] 15:51
> four golden signals of monitoring are latency, traffic, errors, and saturation.


### id699756112
[[2024-03-29]] 15:56
> Latency
> The time it takes to service a request. It’s important to distinguish between the latency of successful requests and the latency of failed requests. For example, an HTTP 500 error triggered due to loss of connection to a database or other critical backend might be served very quickly; however, as an HTTP 500 error indicates a failed request, factoring 500s into your overall latency might result in misleading calculations. On the other hand, a slow error is even worse than a fast error! Therefore, it’s important to track error latency, as opposed to just filtering out errors.

- [n] Error and success latency are interesting metrics to watch out for  * [View Highlight](https://read.readwise.io/read/01ht5zrch0ksrycqexjbebbzh8)


### id699756801
[[2024-03-29]] 15:57
> Traffic
> A measure of how much demand is being placed on your system, measured in a high-level system-specific metric. For a web service, this measurement is usually HTTP requests per second, perhaps broken out by the nature of the requests (e.g., static versus dynamic content). For an audio streaming system, this measurement might focus on network I/O rate or concurrent sessions. For a key-value storage system, this measurement might be transactions and retrievals per second

- [n] Http request per second, network I/O, concurrent sessions, transaction per second,  * [View Highlight](https://read.readwise.io/read/01ht5ztpsxsbwps7e7bf5vf835)


### id699758444
[[2024-03-29]] 16:20
> Errors
> The rate of requests that fail, either explicitly (e.g., HTTP 500s), implicitly (for example, an HTTP 200 success response, but coupled with the wrong content), or by policy (for example, “If you committed to one-second response times, any request over one second is an error”). Where protocol response codes are insufficient to express all failure conditions, secondary (internal) protocols may be necessary to track partial failure modes. Monitoring these cases can be drastically different: catching HTTP 500s at your load balancer can do a decent job of catching all completely failed requests, while only end-to-end system tests can detect that you’re serving the wrong content

- [n] 2xx vs 5xx error rate, any request above 1 second
   Best to track this in load balancer  * [View Highlight](https://read.readwise.io/read/01ht60bvsd0n73n9kndq7anxsr)


## New highlights added March 29, 2024 at 8:10 PM
### id699844552
[[2024-03-29]] 19:55
> Saturation How “full” your service is. A measure of your system fraction, emphasizing the resources that are most constrained (e.g., in a memory-constrained system, show memory; in an I/Oconstrained system, show I/O). Note that many systems degrade in performance before they achieve 100% utilization, so having a utilization target is essential.


