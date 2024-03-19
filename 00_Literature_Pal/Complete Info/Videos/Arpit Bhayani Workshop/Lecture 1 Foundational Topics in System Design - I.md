---
tags:
 - people/pal
 - date/2024-03-18
---

[https://drive.google.com/file/d/15IjLdzLuwYpoGLMevR750tt6RAY3unVX/preview](https://drive.google.com/file/d/15IjLdzLuwYpoGLMevR750tt6RAY3unVX/preview)

# Intro

![Screenshot 2022-12-03 at 9.02.44 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fc472e49-4e56-4a12-8afd-a068c427ca43/Screenshot_2022-12-03_at_9.02.44_AM.png)

![Screenshot 2022-12-03 at 9.05.25 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c987875-2197-4996-81f5-b1b088edcfd9/Screenshot_2022-12-03_at_9.05.25_AM.png)

revise regularly - every week linked to the previous week - exponential increase

![Screenshot 2022-12-03 at 9.08.05 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/283ad26f-af15-4007-9b9e-437cc85f3d4c/Screenshot_2022-12-03_at_9.08.05_AM.png)

![Screenshot 2022-12-03 at 9.08.58 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5b67b6ba-2477-4077-811b-24489f2e7453/Screenshot_2022-12-03_at_9.08.58_AM.png)

# Online Offline indicator

![Screenshot 2022-12-03 at 9.12.57 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ae4f9938-f255-44f3-b079-a859ac1ee224/Screenshot_2022-12-03_at_9.12.57_AM.png)

## 2 ways to approach system design

### Spiral

![Screenshot 2022-12-03 at 9.14.50 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b5168383-f10b-4817-8e61-a2ecf4b0b6fb/Screenshot_2022-12-03_at_9.14.50_AM.png)

- pretty simple and works with systems that are less ambiguous - you typically know what to do when something happens
- e.g. start with a certain core (e.g. database, communication protocol - e.g. for chat, know that WebSockets will be there) and then build things around it in a spiral manner
- for “simple” systems
- The system should be predictable or you have past experience in building similar systems

### Incremental

- not solving for million users on day 0
- you don’t know what requirements you need to adhere to in 2 months
- the problem statement/system you’re designing is very ambiguous
- start with a very simple day 0 architecture, then keep rearchitecting based on what is the bottleneck based on simulating load on every single component
- always think about implementation, don’t think about designing blocks - how will you write code for that system
- Pick the one that works for you and your use case

## Points to remember when designing systems

![Screenshot 2022-12-03 at 9.19.11 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/673e8d80-c03b-44ed-bf47-f9f2734bed07/Screenshot_2022-12-03_at_9.19.11_AM.png)

- common mistake - just start designing the system
- another mistake - affinity towards particular tech stack
- go to the depth of every system that you’re working on

### Walkthrough using the example

- Access pattern - key-value
- Interfacing API

## Heartbeats

![Screenshot 2022-12-03 at 9.26.32 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d8515c0d-fd7f-4518-a8c0-cd8e2e374074/Screenshot_2022-12-03_at_9.26.32_AM.png)

- when you start thinking about implementation, you start discovering new problems
- cannot be assured that every time the device of a user crashes, it will send an API call
- user has to send a heartbeat to the backend system
- Why API server doesn’t automatically know?

## Probing the system

### Storage

- things to be stored: integer (userID) and bool (online/offline)
- Whenever you receive an API call for the heartbeat - mark it as true
- if you haven’t received a heartbeat for a long time - want to set the offline indicator to false
- How to decide what is long enough? - this is subjective

![Screenshot 2022-12-03 at 9.31.25 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/01cbd29c-471b-4551-a7c7-e450257958c8/Screenshot_2022-12-03_at_9.31.25_AM.png)

- this affects how we make the API call

### Scale

![Screenshot 2022-12-03 at 9.34.25 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5083ab0c-c591-452e-984a-3910004523ea/Screenshot_2022-12-03_at_9.34.25_AM.png)

- Do some number crunching
- What is the problem then?

![Screenshot 2022-12-03 at 9.40.16 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3455b185-9199-40e1-9783-c7c1148c0b9d/Screenshot_2022-12-03_at_9.40.16_AM.png)

- hypothetically

![Screenshot 2022-12-03 at 9.42.35 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cdc284f1-6de5-467c-94bf-9f6e6f79a5d6/Screenshot_2022-12-03_at_9.42.35_AM.png)

- total size for 1B users now = 800kb

### How to auto-delete?

![Screenshot 2022-12-03 at 9.43.31 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/183d0539-a892-4dcd-9086-eaa0bb097311/Screenshot_2022-12-03_at_9.43.31_AM.png)

- approach 1: cron-job
- approach 2: offloading to the data store

Now we’re converging on our DB - one of Redis or DynamoDB

### Which one to pick?

- Both gives you KV
- Both gives Expiration

![Screenshot 2022-12-03 at 9.46.08 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1bc94a79-8800-43e2-9feb-6b443fe43edd/Screenshot_2022-12-03_at_9.46.08_AM.png)

Factors:

Dynamo DB - gives strong persistence but Redis can give persistence as well

Redis - based on cost, dynamo’s cost model would make us pay model, Redis might be cheaper

Redis - don’t want to be locked into a vendor - dynamo DB is by AWS. Redis is open-source.

Always benchmark for your use case

DynamoDB - fully managed

Future extensibility

Decisions are not purely engineering-driven!

<aside> 💡 Why does vendor locking matter?

</aside>

<aside> 🪴 To become a senior engineer:

</aside>

What happens in the Real-world:

![Screenshot 2022-12-03 at 10.00.05 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/75748df5-5583-4dc6-b441-eede9a9b726d/Screenshot_2022-12-03_at_10.00.05_AM.png)

- designed using web sockets

## Diving even deeper - How is the DB doing?

![Screenshot 2022-12-03 at 10.01.21 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c14eff76-e085-4a55-9180-031da4e5f10f/Screenshot_2022-12-03_at_10.01.21_AM.png)

- 6M writes per minute - read loads are even more
- how much I/O capacity to give to your database - this is capacity planning - what is the h/w configuration?

### Improving it - Connections Pooling

![Screenshot 2022-12-03 at 10.02.37 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c9b138ff-13a4-4b0a-88e5-1a1b5ae6364f/Screenshot_2022-12-03_at_10.02.37_AM.png)

- can simply scale up the DB - but it would be very costly
- there are other optimizations present like Connection Pooling
- how does API server update in DB?
- Because establishing TCP connection requires 3-way handshake - setting it up is very expensive, every other step is very fast.
- How can you make it better? - Connection Pooling
- From your server, instead of creating 1 connection for every request. When the server has boot up, create 10-15 connections by default and put them in a queue (connection pool is a queue). When you need to make an update, take a connection out of the queue, fire the query, and put the connection back in the queue - reusing connections.
- One simple optimization!
- Can set up min (e.g. 2) and max (e.g. 20) number of connections
- Suppose we make 20 connections but server is not even using it?

Understanding the pattern that can be reused for other systems

- e.g. failure detection!

# 6 things that you need to consider to design any system

![Screenshot 2022-12-03 at 10.30.32 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/23990baf-66e7-439c-8c4b-f6025bc01840/Screenshot_2022-12-03_at_10.30.32_AM.png)

Database and Caching covered today!

## Database

users

id, name, email, bio

blogs

id, author_id, title, body, created_at, updated_at, is_published

![Screenshot 2022-12-03 at 10.32.25 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cc141d40-8d94-4dee-9c08-3d3d377a0980/Screenshot_2022-12-03_at_10.32.25_AM.png)

- Now we’ll discuss the importance of each of these

### Soft delete

- Why use `is_deleted`?

### String data types

- Body and Bio
- A row should be of a `fixed length` so that it knows that location X to location Y belongs to the `name` field, location Y+1 to location Z is `bio`, etc.
- there are two string types - LONGTEXT and VARCHAR
- DB has evolved - do read how they are handling string types - you get a decent boost from understanding this

### DateTime fields

- DateTime: usually has some standard format - DB would store in some format so that it can represent any day. Depending on the DB (MySQL, PostgreSQL), they have their own serialization techniques.
- How it is stored, the exact string is dumped on the disk
- How would the database eventually run a query involving date/time in this model?
- This is why many people use epoch seconds - stores time as integer - one value takes 4B instead of 20B (that is required in the previous case)
- Thus, important how you define the data type - in terms of computation, performance, etc.
- We can use any custom format that suits our use case!

## Caching

- very big misconception on what is this

### What is it, really?

- literally anything that saves you a heavy computation
- most people think it is in memory
- it is literally anything that saves you a heavy computation
- this will simplify our thinking
- once you’ve computed something, don’t recompute
- 100s of other places where this would prove to be more beneficial apart from RAM to cache your data

![Screenshot 2022-12-03 at 11.02.58 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/af043679-fc07-4b3a-97fd-543d7939a853/Screenshot_2022-12-03_at_11.02.58_AM.png)

### A typical way to foresee if you need it or not

- if you need to reuse what you’ve already computed
    
- if you are caching when you are not going to reuse, you will slow down your system
    
- e.g. need to use profile info: few writes, many reads. Saves Disk I/O or CPU computation or expensive network I/O
    
- one standard way to implement: centralized
    

### When is it useful?

Only useful when the time for API to fetch from cache is significantly smaller than the time to fetch for API from DB

### Summary

- are there things that you’re repeatedly accessing? if not, it is a waste of time, CPU resources and memory to incorporate caches
- The overall cost of making an API call to the cache must be at least 2X faster than making an API call to the DB, you don’t know how the cache will perform in different scenarios. So, know your numbers.
- He has deliberating removed caches from 3 systems that he had designed and had seen a performance boost.

<aside> 🚠 Senior Engineers question every single decision, number, what is backing your decision.

</aside>

![Screenshot 2022-12-03 at 11.11.06 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8805bb55-d120-4879-924d-d309133fd26f/Screenshot_2022-12-03_at_11.11.06_AM.png)

Fun exercise (TBD tomorrow)

- Places where it can be used:

# Key Takeaways/action items from the session

- there are two ways of approaching system design:
- Instead of diving straight into designing a system, one should identify the core access pattern at first and avoid bias towards using any tech stack. Instead, go for the stack that meets the requirements. This will help build your intuition for designing systems.
- Start thinking about how you’ll code it right away as opposed to thinking of components as just blocks. For e.g. how will you store the data to achieve the functionality that you want?
- Project the system working at scale to identify bottlenecks. Possible bottlenecks could be in storage (takes too much memory) or compute/load (too many concurrent connections)
- When it comes to deciding which framework/tool/stack to choose (if you’re left with multiple options meeting the criteria above), your decision can be based on one or more factors that don’t have to be purely engineering-driven. E.g. you might want to choose a managed service because you don’t have the bandwidth or humanpower to manage a self-hosted infra. Other factors include future extensibility, avoiding vendor lock-in, cost, support for persistence,
- When the load on a DB has increased, there are optimizations like Connection Pooling that one can do which can give a strong performance boost instead of simply scaling up the DB which is much more costly.
- There are 6 things that one needs to think about while designing a system: database, caching, scaling, delegation, concurrency, and communication.
- Always prefer to do soft-delete instead of hard-delete because soft-delete enables recoverability, archivability, and auditing. From an engineering perspective, hard delete is more expensive too. Plus, you don’t want to let go of all the rich data that the user has provided which can be used for training machine learning models.
- Understanding how different string types truly work under the hood (VARCHAR vs LONGTERM) and how DateTime values are usually stored along with the more performant alternatives that exist can give a critical performance boost.
- Finally, when it comes to caching, it is important to first evaluate if it is even worth doing. This means, there must be some data that we are repeatedly querying (and updating less frequently) and it saves either disk i/o, network i/o or CPU compute. e.g. in a centralized API cache, the boost must be at least 2X of the time required to query the database. Get your numbers!