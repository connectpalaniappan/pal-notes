---
tags:
 - people/pal
 - date/2024-03-18
---

![Screenshot 2022-12-11 at 9.06.26 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a572bb18-9085-4730-8a4a-a97192e015b9/Screenshot_2022-12-11_at_9.06.26_AM.png)

# Non-Relational DBs (NRDBs)

- RDBs need to be compliant. And so, whatever we discussed in the last class applies to all RDBs. But there is no standardization in NRDBs. So, it is up to the implementor for however they want to implement it. So, can’t cover all of them.
- What he’ll cover: go through all the categories of NRDBs to understand when and where to use them, and some internals that make them special, which will help us make the right decision for which DB to pick, when, and why.

## Introduction - busting some myths

- In general (applicable to 60-70% of NRDBs) they give scalability, availability but they compromise on consistency

<aside> 🏋‍♀️ The most important statement to remember

SQL DBs do scale as well. NoSQL DBs also scale. The world is not binary. Both of them are good at their own stuff.

Anything that shards, scales.

Otherwise, Zerodha and Razorpay won’t work. Zerodha is still a single monolithic DB. Razorpay - 80% of their workload is still on RDBs.

</aside>

Then, why are people saying that?

- When people say that NoSQL scales, what they mean is that they give up on some guarantee.
- In CS, every single thing is a tradeoff. You get something, you lose something.
- Always ask yourself: which constraint/property is the DB dropping to gain a different capability? This is what makes them scalable.

## Types of NoSQL DBs

- No fixed line that separates KV stores, Document DBs, etc.
- The lines are very blurry as every DB supports everything as they are evolving and building new features. So, depending on the DB you are using, this might not hold true.
- So, important to understand what a DB could offer.

### Document DB (DDB)

![Screenshot 2022-12-11 at 9.13.42 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/75925d09-6982-4cdb-bb36-bf890fda7bb6/Screenshot_2022-12-11_at_9.13.42_AM.png)

- They are very close to RDBs, `typically` JSON-based.
- RDB: you insert a row. DDB: you insert a document
- Similar to RDB, you can create indexes and do complex queries like aggregation like SUM, COUNT, MIN, MAX, etc. (e.g. ElasticSearch is known for its aggregation).
- This is an advantage for DDBs as one reason that people use RDBs is that you can fire aggregation queries
- MongoDB - horizontal scaling comes out of the box

<aside> ⛳ Extremely crucial feature: You can fire partial updates to a document

</aside>

<aside> 💡 TIP

When a company wants to move from RDBs to NRDBs, they typically move to Document DBs as you almost get all the benefits that you got from RDBs

</aside>

### Key Value Store

![Screenshot 2022-12-11 at 9.16.47 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/22607b93-6eb4-460f-b700-7ea46f7bbeff/Screenshot_2022-12-11_at_9.16.47_AM.png)

- This is a very limited data store because all operations are key-bound: GET key, PUT key, DELETE key
- But precisely because of this, we can heavily share the database by key.
- DynamoDB - KV store which looks like a DocumentDB (a callback to the same point that there is no standardization and everyone does everything)
- Since the operations are key-based, you never see aggregation queries (like MIN, MAX, SUM, COUNT, etc) as it is not meant for that (the sum of all keys for example would have to sum across multiple shards). You limit something. You gain something.
- Understand the DB you are using and the guarantees it is providing.

### Column-oriented DBs (CODBs)

- C-Store - foundational paper on columnar DBs (recommended to read)
- They exploit the internals of DBs very well
- They structure the data in a column-wise fashion

**Row-oriented vs column-oriented**

- How row-based access based in RDBs
    
- A different use-case
    

When to use it?

- When you are going to use only a few columns w.r.t. all the columns available
- For gigantic analytic use cases, like data warehouses (e.g. AWS RedShift, Google BigQuery)
- It is very common to have 100-150 columns, even 1000 columns in a data warehouse
- Don’t want to waste CPU cycles reading data that we are anyways going to discard

When to not use it?

- This would be extremely inefficient for `SELECT *` type queries - they would be extremely inefficient.

Has a small overlap with Cassandra (explore it)

- They do 2-level aggregation (row-group and column-group)
- They take a hybrid approach to make it transactional

<aside> 💡 The performance of a database depends on the storage layout of it. How are we actually storing the data

</aside>

### Graph DBs (GDBs)

![Screenshot 2022-12-11 at 9.39.54 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e15e8b2a-fdda-4022-84cc-7c857ace4f6d/Screenshot_2022-12-11_at_9.39.54_AM.png)

- Simply, the graph data structure put onto a DB
- When you look at any problem, it can be modelled as a graph application

<aside> 💡 Every single use case in the real world can be stored in the form of a graph DB

</aside>

- But should we?

Transactional vs analytical vs graph use cases:

- What do they give? Ability to fire graph algorithms (e.g. shortest path first, traversal, identify missing edges, least common ancestor, etc.)
- Downside:

<aside> 💡 If you need to use graph algorithms, you don’t have any choice but to use graph DB

</aside>

- Usually, they are used as an auxiliary DB, not the main transactional DB (e.g. use RDBs for that)
- Example 1: Amazon needs to build a recommendation engine.
- Example 2: Fraud detection

<aside> 🥇 Final words of wisdom

</aside>

## Why do people say NoSQL DB scales but SQL DB doesn’t?

![Screenshot 2022-12-11 at 9.49.32 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/90b1fc44-d082-4bc6-b3b5-526f32214246/Screenshot_2022-12-11_at_9.49.32_AM.png)

- NRDBs don’t have relations
- We are denormalizing the data in NoSQL.

<aside> 🥇 Thus, don’t have simplistic notions of X scales, Y doesn’t scale. Understand why they are able to scale. Crack the surface and go deep to understand. Understand which type of queries are performant in the given DB and use the DB for that use case.

</aside>

## When to use SQL DBs vs NoSQL DBs?

![Screenshot 2022-12-11 at 9.53.37 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4895b551-1029-4289-b890-b8206e292417/Screenshot_2022-12-11_at_9.53.37_AM.png)

RDBs when:

- When you know that all your data can reside in one DB. Even if you’re sharding your DB, you can accommodate your data in a single node and all your queries can operate within the same shard.
- You need ACID - helps ensure your data consistent, etc. Which is why most payment systems use RDBs.
- When you need relations, constraints, integrity checks - you cannot afford the data going into an inconsistent state and losing its integrity

NRDBs when:

- You don’t need relations at all and you don’t need foreign key checks.
- When you don’t need strong consistency and eventual consistency would work

<aside> 💡 Align yourself to the organization as opposed to aligning organization to your tech stack

</aside>

Question: Why would people want to store denormalized data and maintain redundant copies of the same data?

Question: What about schema versioning - that we get in the form of migrations in RDBs but not in NoSQL DBs?

Tools for sharding:

## Advice for when you’re starting out

- When you don’t have a clue starting out a company, what DB should one go ahead with?

# Designing Slack’s Real-time Communication

Focus:

- what happens when you send a message
- how do you broadcast
- how do you scale it to millions of users

Bonus: Zoom Chat, WhatsApp also

Takeaway: understanding one in detail makes it trivial to adopt it for others

## Requirements

![Screenshot 2022-12-11 at 10.10.55 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63c6a696-affc-459c-aa19-d5621dc042a2/Screenshot_2022-12-11_at_10.10.55_AM.png)

- extends to real-time systems (e.g. any kind of creator tools)

![Screenshot 2022-12-11 at 10.11.46 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/33b79661-b615-4626-b780-00c38a1ce95b/Screenshot_2022-12-11_at_10.11.46_AM.png)

## Schema

- Don’t go into specifics of whether it is a SQL DB or NoSQL DB when drawing the schema
- What it means: the entity has the particular attributes

4 entities: `messages`, `users`, `channels`, `user_channels`

### V1

### Improving it

- Is `user_channels` a good name?
- Is simply using `destination_id` which can be either `channel_id` or `user_id` future proof/good?
- Can we use a simpler way instead of adding both `destination_id` and `type` to `membership` that is more seamless, more natural?

### V2

## High-level design

### Create a DB cluster

- Messages have a tendency to explode, thus, we have to think of horizontal scalability out of the box and one DB won’t be able to hold the data which is why not going with SQL DB. This applies to any situation where you know there is going to be BigData.
- e.g. Cassandra cluster because messages don’t have a foreign key relationship as messages of one channel can lie in one shard
- How to read a message?
- Given the scale of Slack messages, you want to use a DB that gives sharding/partition - gives pagination + ability to fire retrievals on a particular shard

### Create API server

- For auth, payment, channel information, etc. (not real-time communication related)
- They talk to the DB cluster

### Communication layer

- When a user is trying to send a message, how would you approach it? What to add in the middle?
- Add a WebSocket server (let’s call it Edge Server or ES) in the middle as we need to support real-time communication

### Persistence - the issues

- When user A sends a message to the ES, does the ES send the message directly to user B? How does it persist the message?
- What is ES? - a normal EC2 machine that understands the WSS protocol
- What does ES need to write the message to the Cassandra DB? DB credentials - need to expose that in the ES

<aside> 🧿 Most of us, when we architect such a system, we don’t think about security. The most important thing is to have the thought that security is important to keep in mind while architecting any system.

</aside>

- What is the responsibility of the ES? What could go wrong if ES tries to write to the DB directly?

### The responsibility and performance implications of WebSocket servers

- One WebSocket server connection is extremely expensive as it requires maintaining a persistent TCP connection with the end user

### Persisting data - solution

- As soon as we think of asynchronously, we use a message broken, like Kafka or SQS, the messages are consumed by some consumer and they write it to the DB.
- What to pick? SQS or Kafka?
- Flow until now:
- Now, should ES send a message to B after it has persisted to DB or right after receiving an ack from Kafka?

### The overall flow till now

### Another challenge with persistence

- Scenario:
- Problem: This is a guarantee that our system needs to provide. We can do eventual only at some places and not all places. Again, these are all tradeoffs.

### 3 ways to persist a message (depending on the system we are designing)

The way we choose determines the guarantee we are promising

The general architecture:

- Scenario 1: Strongly consistent persistence needed (e.g. Slack)
- Scenario 2: Eventual Persistence is okay (e.g. WhatsApp)
- Scenario 3: No message persistence is okay (e.g. Zoom)

<aside> 💡 Depending on the guarantees that your system needs to provide, you need to decide what kind of approach that you take.

</aside>

### Scaling WebSockets

- Why do we need to think about this?
- Suppose (hypothetically)
- Scenario 1: A wants to send a message to B.
- Scenario 2: When there is a group chat between A, B, C, D, and a 5th person E. Since the limit of number of users on one ES in our hypothetical scenario is 4, user E will connect to a different Edge Server.

### Overall architecture

![Screenshot 2022-12-17 at 6.01.59 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b5956068-ea15-4c0a-87ae-fcd75981ee38/Screenshot_2022-12-17_at_6.01.59_PM.png)

# Recommended Reads

- C-Store: seminal paper on columnar DBs
- [Spanner: Google’s Globally-Distributed Database](https://static.googleusercontent.com/media/research.google.com/en//archive/spanner-osdi2012.pdf)

[https://drive.google.com/file/d/1CWv_vbM-OOM9v-pgNmazxvLiic4ErG3d/preview](https://drive.google.com/file/d/1CWv_vbM-OOM9v-pgNmazxvLiic4ErG3d/preview)