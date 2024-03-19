---
tags:
 - people/pal
 - date/2024-03-18
---

[https://drive.google.com/file/d/1ZA-r2VLUssb-Keu_IjT3jAHjCNHEBqZC/preview](https://drive.google.com/file/d/1ZA-r2VLUssb-Keu_IjT3jAHjCNHEBqZC/preview)

![Screenshot 2022-12-04 at 9.05.23 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bc6c93c7-5a2e-483f-8515-10321ec50801/Screenshot_2022-12-04_at_9.05.23_AM.png)

# Caching

## Caching at different levels

### Browser

- static assets: JS, CSS
- Cookies
- Benefit:

### CDN

- static assets
- not saving network calls but it keeps the data near the user
- saving more long network delays gives a perceived perf boost

### Remote centralized cache

- What we spoke about in the last session
- e.g. centralized Redis/Memcache
- this saves DB hits (assuming that fetching from the DB is slower)
- anything that is centralized and can be used via an API
- e.g. if you put something on S3 and everyone can access it, S3 is also acting as a cache. Doesn’t have to recompute. Anything that prevents repetitive computations is a cache.

### DB

- How will you really do it?

<aside> 💡 This is where the gap in our understanding is if we aren’t able to answer it

</aside>

- What is a DB actually work? - it is a server running in a virtual machine with some RAM, and a particular port is exposed where it is running
- Every DB has a separate memory buffer (often called query buffer pool or buffer pool - for MySQL)
- Before a particular segment of the disk is used, it is cached in memory on the server instance itself
- Java application - we can specify `min` and `max` allowed memory - which allows using memory to do faster computation instead of relying solely on the disk.
- Buffer Pool - what does the DB choose to store here?
- This does not mean that the data will not be persisted in the disk, indexes will still be stored on disk but it is just cached in memory, and invalidation, etc. kicks in as needed but the idea is to save an expensive disk i/o

![Screenshot 2022-12-04 at 9.22.11 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b2eabb5d-b453-411b-bdaf-1cb2300fe4d7/Screenshot_2022-12-04_at_9.22.11_AM.png)

### DNS query cache

- at the browser’s end and the DNS server’s end
- So that you don’t always have to make multiple calls to multiple routing servers / the global DNS system to find the IP corresponding to the website!

### Local disk of the API server!

- suppose a big file was queried
- the next time it was queried, just do a checksum to see if the file was modified
- if it was not modified, just return the cached file from the disk rather than doing the expensive query again
- One problem with this:
- Example:

### Materialized Views

- saves repetitive joins on the tables in the DB: [https://www.geeksforgeeks.org/differences-between-views-and-materialized-views-in-sql/](https://www.geeksforgeeks.org/differences-between-views-and-materialized-views-in-sql/)

## Best practice

One good way to think about different types of caching:

- Start from one extreme end
- Left side: user, right side: database - heavier computation is usually done on the database end and lighter computation is done on the user side. So, more caching on the user side is usually done. So that users have a great experience!

<aside> 🚀 Whatever component you have (browser, API gateway, load balancer, API server disk, API server RAM, centralized remote cache, DB cache using buffer pool, materialized views), always try to avoid making requests to the next level of your infra. For every single H/W component of your infra, you can cache something. Depends on your tolerance level and how fresh you need the data to be.

</aside>

# Scaling

![Screenshot 2022-12-04 at 9.36.17 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/91599d9f-e85f-421a-a1a5-1a91a562a8cb/Screenshot_2022-12-04_at_9.36.17_AM.png)

- handling concurrent requests is what matters the most, no X number of users in one day or one hour - what matters is at the same instant

## Vertical Scaling (VS)

- simply add more resources on one instance - more RAM, compute

### Disadvantages

It has a limit. i.e. I might be able to say that I want 32 GB, 64 GB, 500 GB RAM, but not be able to ask for (say) 1 TB!

But why? What is stopping us from doing that?

Remember Computer Architecture classes

If a phone has expandable storage (256 GB), what will happen if you try to add a 512 GB memory card? It will not accept it.

There is a H/W limitation

For a device that supports 256 GB, if you insert 512 GB card, they both are incompatible at the H/W level

This applies to Vertical scaling too - if the virtual machine instance only supports 2 TB of RAM, you cannot plug in 5TB RAM!

When you hit the limit in vertical scaling, the only option left is to go to Horizontal scaling!

## Horizontal Scaling (HS)

![Screenshot 2022-12-04 at 9.37.10 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f47fa2be-651d-4bd3-bee5-98bd7ee4f49a/Screenshot_2022-12-04_at_9.37.10_AM.png)

- You add multiple instances of the same configuration and add a load balancer in front of them

### By-products

- fault-tolerance
- Linear amplification

## Good scaling plan

![Screenshot 2022-12-04 at 9.42.06 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a481fe98-d542-4a36-a3e5-5720a1cbacbf/Screenshot_2022-12-04_at_9.42.06_AM.png)

- At the initial stage of a startup - don’t go for HS, typically VS until a certain limit, and then you do HS after that. No pre-mature optimizations. Trying to do HS can add a lot of unnecessary complications as no one knows if the company is going to survive.
- You don’t have to scale on day 0

<aside> 💡 Engineering does not drive business. Business drives Engineering for an early-stage startups (typically). Don’t make random assumptions. Business comes first, tech comes second. Context is important - use your mind before taking the call

</aside>

![Screenshot 2022-12-04 at 9.44.59 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d8cb85c8-9fcc-4e5f-864e-f207d6423e6c/Screenshot_2022-12-04_at_9.44.59_AM.png)

### Caveats with Horizontal scaling

Can you keep horizontally scaling infinitely?

- the catch: you might have horizontally scaled your API server but your DB has not been scaled, or the cache hasn’t been scaled
- Most brittle parts of your system

## Scaling DB

![Screenshot 2022-12-04 at 9.51.04 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/35da0b9c-e24b-40e9-8ea1-89bb1ca68b19/Screenshot_2022-12-04_at_9.51.04_AM.png)

- Zerodha still uses monolith DB instance - no sharding, partition - keep it simple

<aside> 🤔 As long as things are running, don’t need to change it

</aside>

- Usually: vertical scaling up till a point (keep it as simple as possible) and if needed, then consider 2 different use cases.

### Read-heavy application

if seeing a lot of reads compared to the writes (if the use case is read-heavy)

- create read replicas
- how to do it?

### Write-heavy application

If one master is not enough to handle all write requests, you shard your database

- e.g. 3 mutually exclusive slices of the database and each master can have its own replicas and the API server has to connect with all the shards and replicas
- we have to write the code for which API is directed to which shard or replica
- We have to decide how to shard, where to hit, etc. No magic / single way of doing it
- think about implementation (e.g. who/what will tell the API server which connection to use)
- For some databases, support for this kind of routing comes out of the box: MongoDB cluster, Cassandra, Redis cluster

### Hot-swapping and chaos monkey

- If a single machine is used for a really long time, its performance can get degraded due to overheating
- So, if you have horizontal scaling set up, Cloud providers automatically detach the instance from the load balancer and a new machine will be added. This way VMs are hot-swapped without changing the IP address. This is called `hot-swapping`.
- You can also configure a `chaos monkey` such that an instance is terminated randomly after some time to ensure that application performance is not deteriorated with hardware deterioration. In this case, setting up of the new instance should be optimised using containers so that the image is pre-built and thus, booting time is minimal.

# Delegation

![Screenshot 2022-12-04 at 10.06.52 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/50823dd7-4447-4838-b4bc-a95d786b0c63/Screenshot_2022-12-04_at_10.06.52_AM.png)

- one of the most underrated ways to get perf optimization
- one key thing that everyone appreciates hotstar for the seamless streaming:

<aside> 🚠 Key principle: What does not need to be done in realtime should not be done in realtime. Thus, whatever you can delegate, delegate it.

</aside>

- E.g. say you want to render a profile on medium and show how many essays a user has. What to do?
- Instead of counting it on runtime, keep a variable for the count. Whenever a post is published, asynchronously make count++.
- What can be delegated?

## Message Brokers

- What makes delegation possible: message broker

![Screenshot 2022-12-04 at 10.13.02 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5210e8bd-903a-43f5-aed6-e75235cfb2ee/Screenshot_2022-12-04_at_10.13.02_AM.png)

### Message queues

- you send a message, it sits at the back of the queue
- In the image above:
- when a consumer completes processing a message, it deletes the message from the queue
- this is pull-based (not push-based) as a consumer is making the API call and asking for the message
- here, consumers are homogenous - i.e. it does not matter to which consumer the job goes as every consumer is almost the same and does almost the same thing.

### Message streams

![Screenshot 2022-12-04 at 10.16.28 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/808b83f4-695e-4577-b479-225058f18a40/Screenshot_2022-12-04_at_10.16.28_AM.png)

- it is possible that the same message needs to be consumed by different types of consumers
- E.g. when a blog post is published: we want to index that entry in the search service and want to update the number of total essays
- use message streams
- each type of consumer can have multiple consumer instances
- each consumer type goes through each message sequentially
- no pressure of consuming quickly
- extremely beautiful for building decoupled systems
- Kafka made it very popular

### Pub/Sub

Not covered in this class but it is also a message broker. More info here: [https://www.bmc.com/blogs/pub-sub-publish-subscribe/](https://www.bmc.com/blogs/pub-sub-publish-subscribe/)

| --- | --- |

### Example

**Setup**

![Screenshot 2022-12-06 at 9.07.48 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/373d6d65-749d-4532-af11-d41318c11b08/Screenshot_2022-12-06_at_9.07.48_PM.png)

**Using Message queues**

![Screenshot 2022-12-04 at 10.18.25 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/73caf967-cd93-4c5a-ae1d-60beb8e166e5/Screenshot_2022-12-04_at_10.18.25_AM.png)

- here, the entry is made in the database directly if this is the first time that the user has published
- simultaneously, send the on_publish event to SQS and each worker basically updates the blog post count in the profile table in the DB async

**Using message streams**

Now, along with incrementing the count, we want to index it in search.

![Screenshot 2022-12-04 at 10.18.58 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c289bef7-28ea-446a-bbe2-726fcca48082/Screenshot_2022-12-04_at_10.18.58_AM.png)

- reusing message queues:
- Instead, use message streams

## Kafka (message stream) essentials

![Screenshot 2022-12-04 at 10.21.39 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/213ba5d6-3988-417d-baf0-31f5f98cdc0a/Screenshot_2022-12-04_at_10.21.39_AM.png)

- holds true for Kinesis / any other message stream
- When you create a Kafka topic (everything is a topic in Kafka, topic is the 1st level entity for Kafka - e.g. blog_published, tweet_posted, tweet_liked)
- You send a message to the topic (with details like who published the blog, blog ID, etc.)
- For each topic, there are multiple partitions
- One consumer type can consume from multiple partitions
- Partitions determine the concurrency of the systems
- Ordering of messages is at a partition level
- e.g. 3 partitions, 5 search consumers
- Global ordering of messages is not supported by Kafka (only partition level)
- On Kafka, there is a deletion policy (e.g. after 30 days) but not after reading a message
- the group of consumers of the same type is called the `consumer group` e.g. analytics can have 4 consumers, search can have 3. There can be n types of consumer groups but each can have only K number of consumers consuming from them. K being the number of partitions!

### Committing

- It is possible that in a queue you have 5 messages. When the consumer reads from the queue, it will read the first message and then, it makes a commit.
- Then, when it reads from the queue again, it reads the second message. But before committing, the server died.
- So, when it reads again, it starts from the last committed message and so, starts from the second message again.
- So, it is possible that the same message is processed multiple times in Kafka. And that is okay.
- Kafka supports `at-least once` guarantee and not `at-most once` guarantee.
- Never commit before you’re done processing the message

# Concurrency

We’ll go in depth of this next week.

### Why is it super important?

- Because the number of cores in the hardware are increasing
- We want to get the max out of our h/w as h/w costs money
- Because there are many cores lying useless on our machine, we want to leverage concurrency to make processing faster and leverage h/w better

## Standard ways of doing that

Use threads and multiprocessing

![Screenshot 2022-12-06 at 9.35.37 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dd2c9ced-ac2a-448b-aae6-d6fa184b9ac3/Screenshot_2022-12-06_at_9.35.37_PM.png)

## Issues with concurrency

![Screenshot 2022-12-06 at 9.46.32 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4bb117c1-209c-4eff-8a15-4a2959cd97c3/Screenshot_2022-12-06_at_9.46.32_PM.png)

- communication between threads:

## Handling concurrency

- To solve such issues we use mutexes and locks on the critical parts
- overall: use locks wherever there is contention
- an advanced way of doing it: [CRDT](https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type)
- the most common thing to definitely know is pessimistic blocking - which will be covered in depth later in the course.

![Screenshot 2022-12-04 at 10.48.26 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f8c234e7-c437-4fdd-99e1-50e2d41b33b0/Screenshot_2022-12-04_at_10.48.26_AM.png)

- here, multiple people are triggering count++. if initial count is 10, and both of them trigger clap at the same instant and even if both of them are able to operate on the same count variable, both of them will leave the variable at 11, when it should have been 12.
- contention - multiple people can act on the same data entity - consider putting it into transactions or use atomic instructions - otherwise it will lead to inconsistency. (we’ll touch upon this in the next week)
- What is consistency? The final value has to be the same in every possible circumstance

# Communication

![Screenshot 2022-12-04 at 10.50.59 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/90e70049-3a14-4cb6-b1ce-9cd6257d85d7/Screenshot_2022-12-04_at_10.50.59_AM.png)

- communication is how the end user will talk to your system
- the end user could be anyone
- typical: client-server paradigm based where the server does the heavy lifting

## Short-polling

- typically done when we are anxious
- e.g. we have created an EC2 instance and are constantly refreshing to check if instance has started or not (we could manually refresh or JS could repeatedly make API calls through setInterval) - this is called short-polling.
- this can put a load on the backend server and database but gives better UX as the user doesn’t have to refresh manually + lots of requests and responses.

## Long-polling

![Screenshot 2022-12-04 at 10.56.43 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/82f9b159-f80f-4371-89f3-e110a9f5ce1e/Screenshot_2022-12-04_at_10.56.43_AM.png)

- disadvantage of short-polling:
- in long polling, the server says:
- makes sense to remove the request loop from the client and add the loop on the server
- the server is continuously polling the database to check if something has changed
- Here, we are reducing the number of HTTP requests made from the client to the server
- The client should make only one request and get only one response
- It is possible that the server took a lot of time, which leads to a Timeout error. Then, need to request again and wait for the response again.
- We have to implement it - no magical way to do it.
- It is not that common.

## Short-polling vs long-polling

![Screenshot 2022-12-04 at 10.58.24 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c1c40591-2436-40bc-a316-a1f2c25324cc/Screenshot_2022-12-04_at_10.58.24_AM.png)

- in cricket, long polling - only returns a response when the next bowl is bowled whereas in short polling, even if the next bowl is not bowled, it will keep making requests and keep receiving the same value.

## WebSockets

![Screenshot 2022-12-04 at 10.59.42 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4996f350-8ac1-4f03-a446-416473ee3069/Screenshot_2022-12-04_at_10.59.42_AM.png)

- This is more common
- E.g. chat application - if a message is sent from user A to user B, I want the message to immediately reach the user B. The server has to proactively send a message to user B instantly.
- The server should proactively send data to the client instead of the client polling the server
- Need a bidirectional channel open - once connection has been established, it stays open forever until someone actively disconnects it or there is a network aberration
- Once the connection is established, the server can send messages to the client without any polling from the client.
- Use cases (live experiences) - chat application, live streaming, zoom chat, multiplayer game, anywhere you need to do real-time communication
- Very low communication overload - as once the communication channel is established, only about sending the actual data and receiving the actual data. Otherwise, for every connection that we create, 3-way handshake to establish TCP and 2-way teardown.

## Server-sent events

![Screenshot 2022-12-04 at 11.03.14 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ede521ac-0b1d-4919-b93d-f6a6d802583a/Screenshot_2022-12-04_at_11.03.14_AM.png)

- this is half of WebSockets (which is bidirectional but this is unidirectional)
- here, only the server can send data to the client
- the client cannot send anything to the server - which can be an advantage (reduces bunch of overhead in the protocol) as well as disadvantage
- e.g. stock market ticker - the client is not requesting for latest data, the server is proactively sending it to you
- MDN documentation is really good for server-sent events
- Another application: deployment logs
- Why not use websockets instead?

## Example

![Screenshot 2022-12-04 at 11.06.00 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8dbcc903-814d-4c05-8108-5b6c92a2d744/Screenshot_2022-12-04_at_11.06.00_AM.png)

![Screenshot 2022-12-04 at 11.08.50 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8ed9969e-8e64-4894-a15c-227c7745df7c/Screenshot_2022-12-04_at_11.08.50_AM.png)

- persistent TCP via connection pooling
- like count changing on the fly - proactively sent to the client over websocket

## Overall

- short-polling is already the most common
- implement long-polling one and build WebSockets and server-sent events to learn
- start building understanding around communication and implement it

# Questions

- Difference between server-sent events and long-polling
- How do you maintain persistent TCP connections on serverless?