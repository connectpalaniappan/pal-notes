---
tags:
 - people/pal
 - date/2024-03-18
---

![Screenshot 2022-12-10 at 9.04.36 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b4da52a9-14b3-4c29-8709-bb8cdcb8b359/Screenshot_2022-12-10_at_9.04.36_AM.png)

# Intro to Relational Databases (RDBs)

extra special because of the strong guarantees that they provide - ACID (refer to pre-reads) irrespective of whatever other DB options come out there

- They store data in BTrees
- Data is represented visually as rows and columns. Why?
- When you’re thinking about the next technological breakthrough, keep track of financial applications - you’ll likely get to know it!

## How to execute a query?

- One naive way is to go through each row sequentially. But this linear scan will increase the time to execute the query
- Whenever reads as slow, we create indexes to make reading faster (that is the only role of indexes) (refer to the pre-reads to learn about indexes)

## Database locking

![Screenshot 2022-12-10 at 9.11.03 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e55052ce-6ce9-4c74-acda-ad503a2f5d07/Screenshot_2022-12-10_at_9.11.03_AM.png)

- Databases allow you to set locks on rows that are being accessed concurrently
- RDBs provide a way to solve it using `Pessimistic Locking`

## Pessimistic Locking

<aside> 💡 **Core idea**

You are being pessimistic. If I am reading or writing a row, what if someone else is reading/writing in the same row at the same time as well? Thus: protect your critical section with locks

</aside>

### How?

- acquire the lock
- have the critical section where your query / operation is being run
- release the lock

Critical section: row (s) being accessed concurrently

### Example

- Assume there are two transactions coming in trying to update the same set of rows
- We don’t want both of them to update at the same time as it will make the data inconsistent
- What to do?
- This locking is only done for your critical section otherwise DB throughput would be low!
- Use case:

### Why use locks?

![Screenshot 2022-12-10 at 9.14.45 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ac47c8c5-f321-4b42-82b3-9f71194ea1e8/Screenshot_2022-12-10_at_9.14.45_AM.png)

To ensure that our data has:

- Strong consistency
- High integrity

### Risks in using locks - deadlocks

![Screenshot 2022-12-10 at 9.15.54 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d34fe667-5d72-4999-8e34-43d561bafa99/Screenshot_2022-12-10_at_9.15.54_AM.png)

- What does that mean?
- You don’t want deadlocks. When you’re building a high throughput system with concurrency and parallelism, you are risking your system getting into a state of deadlock
- RDBs safeguard us from deadlocks. How?

<aside> 💡 Very important to know how your DB behaves when you throw a lot of throughput at it

</aside>

## Types of locks

### Shared locks

![Screenshot 2022-12-10 at 9.20.09 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/67dc3524-5c72-49aa-b774-71a81485bd71/Screenshot_2022-12-10_at_9.20.09_AM.png)

- When a transaction wants to just read a row, not update it, it can just take a shared lock on the row.
- This way, other transactions can also acquire a shared lock on that row at the same time and read the row.
- If T1 is the first one to acquire the shared lock (i.e. it owns the shared lock), it will get priority to be able to write on that row. No other transaction will be able to modify it. They will have to wait until T1 releases that lock.
- And T1’s lock will have to be upgraded to an exclusive lock to be able to write to the row
- how to implement: end SQL statement with `FOR SHARE`

### Exclusive Locks

![Screenshot 2022-12-10 at 9.25.54 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/464825ec-05da-4cef-9f8a-4bf873981720/Screenshot_2022-12-10_at_9.25.54_AM.png)

- e.g. people used to cheat in exams. But there were people who would try to hide their answer sheets by putting their arms around their answer sheet so that no one else can see their answer
- If I am locking my row using exclusive locks, other transactions can’t even read the row, let alone modify

<aside> 🚀 Here, once the exclusive lock is released, all the other transactions waiting on the lock will reevaluate their query so that they know which row they need to contend for

</aside>

- how to implement: end SQL statement with `FOR UPDATE`

### SKIP LOCKED

![Screenshot 2022-12-10 at 9.30.17 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b41370d4-9fc1-482d-9546-cd96eb3a7bff/Screenshot_2022-12-10_at_9.30.17_AM.png)

- In some cases, it is okay to ignore the locked rows and return only the unlocked rows (covered in an example later below)
- how to implement it? end SQL statement with `SKIP LOCKED`
- Hence, for the previous example, the result of T2 will be 2 rows being returned - 3,4

### NO WAIT

![Screenshot 2022-12-10 at 9.32.04 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6427f078-c232-415f-91b0-8b91c4101e9d/Screenshot_2022-12-10_at_9.32.04_AM.png)

- What if, in the case of any row being locked, I don’t want to wait and want to throw an error immediately as waiting reduces the throughput
- how to implement it? end SQL statement with `NO WAIT`

## Example: Airline Check-in system

### Description

![Screenshot 2022-12-10 at 9.33.12 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/40390de6-4933-4104-beff-d7ebcaa8a6e0/Screenshot_2022-12-10_at_9.33.12_AM.png)

- Check-in system (not booking system, thus, payment already done). Here, just trying to select a seat that they want
- Multiple airlines, each airline has multiple flights, each flight has multiple trips, each flight = 120 seats
- A user is booking a seat on one trip on a flight

### Schema

![Screenshot 2022-12-10 at 9.34.51 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/88830335-a53f-4075-bbfb-37f104f412bd/Screenshot_2022-12-10_at_9.34.51_AM.png)

- When you’re doing a check-in, the `seats` table is getting updated

### High-level architecture (Day 0)

![Screenshot 2022-12-10 at 9.35.36 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bb72ad9f-9242-41ec-a223-3c627472db14/Screenshot_2022-12-10_at_9.35.36_AM.png)

- Check-in service (might involve load balancers and multiple servers), RDB for holding the information, and admin service is taking care of populating seats, managing flight time, etc.

<aside> ⛳ Goal: We’ll see how locking impacts this design

</aside>

<aside> 🌼 Advice: Write code to implement all of this - in whatever language you prefer that supports parallelism and concurrency

</aside>

### Approach 0

- Ask the user to enter their user ID and the seat number that they want. Keep in mind:
- Currently, no checks

### Approach 1

- Allocate a seat at random instead of asking the user for their seat preference
- This is minimizing the problem but not resolving it. We are still not adding any checks. Multiple people can be allocated the same random seat

### Approach 2

- Here, we are using threads to mimic the following use case:
- How is the booking done?
- Result?

### Approach 3

- Change how we book a seat
- Result?
- This case is screaming for locks to be applied

### Approach 4

- Everything same as `Approach 3` + `FOR UPDATE` in the SQL query
- What happens?

<aside> 🤔 Remember it is not that user ID = 1 will get seat ID = 1A as we don’t know which thread will get the CPU first and be able to fire the transaction and execute the query. We cannot predict the result of purely parallelized code as it depends on how threads are scheduled, and how transactions will be scheduled on the database.

</aside>

### Approach 5: Improving performance

- Just add `SKIP LOCKED` to the query
- Here, users just need a seat. Any seat will work. So, we don’t really need to wait for the lock to be released as any other unoccupied seat will work too.
- Simply proceed ahead and ignore the rows that are locked
- Thus, the output should be the same as above with execution time reduced
- In this case, we just need random allocation - so, just skip the locked rows.
- Don’t want the throughput of our system to go down due to contention

<aside> 🚀 This is what matters at scale. Time for execution came down from 1.44 secs to 158 msec!

</aside>

<aside> 🌼 `FOR UPDATE`: ensure exclusivity of all rows and ensure all rows are filled

</aside>

If we had used NO WAIT instead, the transaction would be killed instead.

## Questions

Re-evaluation after locks is released. Does that affect performance?

- Assuming that indexes are in place, the SQL query should be good!
- If SQL queries are not performant, database performance will go down drastically. Thus, always set the indexes correctly.

![Screenshot 2022-12-10 at 10.20.07 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6899be24-fa28-4dd2-ba21-905f31e87144/Screenshot_2022-12-10_at_10.20.07_AM.png)

<aside> 🔑 Fixed inventory (120 seats) + contention (everyone trying to book at the same time) = locking (never forget this). This can be applied to many many systems.

</aside>

# Distributed KV Store

(using only relational databases)

The design is inspired by Redis, Memcache, Apache Ignite and others.

<aside> 🔑 RDBs are the best because of the ACID guarantees that they give - knowing them really well makes you a better engineer. For many use cases, by default, you can model them in RDBs!

</aside>

![Screenshot 2022-12-10 at 10.30.47 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/43dee6d4-6635-4d43-b765-399737e9bcb9/Screenshot_2022-12-10_at_10.30.47_AM.png)

- TTL means that the key should auto-expire
- Brainstorm: for every system, we’ll do a detailed brainstorming

## Schema

- What will TTL be?

![Screenshot 2022-12-10 at 10.33.08 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/70f36809-24e1-49a8-bd3c-81390a4fe72a/Screenshot_2022-12-10_at_10.33.08_AM.png)

- Why `int` for TTL?

### Deletion

`DEL k1`

- How would you delete a key?
- One option: `DELETE from store where key = k1`
- Thus, the query will be: `UPDATE store SET is_deleted = true where key = k1`

![Screenshot 2022-12-10 at 10.49.39 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/983c7f15-8384-4177-a763-8f354d8f3d10/Screenshot_2022-12-10_at_10.49.39_AM.png)

- Is any column redundant?
- Any other optimization on DELETE?

### Upsert

`PUT k, v`

- Problem:
- What can we do?

### Retrieving

`GET k`

- exclude keys which have been deleted or expired
- thus, TTL > current time is enough to handle both the cases
- Here, we have simplified soft-delete and expiration

![Screenshot 2022-12-10 at 5.25.48 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/61624026-0acd-46ea-9a0e-743823a67588/Screenshot_2022-12-10_at_5.25.48_PM.png)

### Overall

![Screenshot 2022-12-10 at 10.59.15 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/17d7eacc-c62c-4a0b-a918-b56feea06c26/Screenshot_2022-12-10_at_10.59.15_AM.png)

## Cleaning up our database - Implementing TTL

### Approach 1: Batch deletion with cron-job

- Every hour - go through all the keys that are expired or soft deleted and hard delete them from the database
- Why are we doing it periodically?

![Screenshot 2022-12-10 at 5.12.01 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fae09067-20e8-455d-b76c-b539d91af71c/Screenshot_2022-12-10_at_5.12.01_PM.png)

![Screenshot 2022-12-10 at 11.02.45 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cfc77ec1-b01b-4f28-9b2a-073d1389a18f/Screenshot_2022-12-10_at_11.02.45_AM.png)

![Screenshot 2022-12-10 at 11.05.46 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0c7a03cc-6250-433f-b706-113b99b07823/Screenshot_2022-12-10_at_11.05.46_AM.png)

![Screenshot 2022-12-10 at 5.25.05 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db5961f8-ef61-4dab-b332-937075a2fa5e/Screenshot_2022-12-10_at_5.25.05_PM.png)

### Approach 2: Lazy deletion

- Another option, how Redis does deletion

<aside> 🧨 This will not work with disk-based databases, only in-memory databases

</aside>

What does it entail?

![Screenshot 2022-12-10 at 11.12.11 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/61a2f54b-cee9-4c25-b9ba-55c69a671fdd/Screenshot_2022-12-10_at_11.12.11_AM.png)

- If a key is fetched from the database and found to be expired, delete it
- Why will it work for in-memory DB? Because deleting a key in memory is much faster and much more efficient than deleting from disk (where rebalancing + disk I/O needs to happen)
- When the key is found to be expired, it goes to in-memory hash table and immediately deletes it
- Edge case

### Random Sampling and deletion

- How to write the job for the periodic deletion mentioned in Approach 2 above?

![Screenshot 2022-12-10 at 11.11.56 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/133214ce-fda6-408b-a0c2-056b31432c4c/Screenshot_2022-12-10_at_11.11.56_AM.png)

- Lazy deletion already deletes (roughly) 80% of the expired or soft deleted keys
- What does Redis do?
- E.g. even for population surveys in India, don’t go to every household. They take a well-informed sample and extend it to the population.

![Screenshot 2022-12-10 at 11.15.12 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/156f296d-d199-4947-8069-b8de3fccd96a/Screenshot_2022-12-10_at_11.15.12_AM.png)

- On disk-based databases, you cannot do random disk I/Os - they are expensive. That is why this approach is meant only for in-memory DBs.
- Why the number 20? It comes from the Central Limit Theorem! a.k.a. math is important in the real world.

![Screenshot 2022-12-10 at 11.16.11 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dabde6b6-b8cb-4106-8972-ae7df775074e/Screenshot_2022-12-10_at_11.16.11_AM.png)

## High-level Architecture

![Screenshot 2022-12-10 at 11.18.00 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bdb0c9dd-e9a5-40b7-b9b1-bc2262d13515/Screenshot_2022-12-10_at_11.18.00_AM.png)

- Start with a single-node MySQL instance - it will be our data store
- We might have bunch of API servers with load balancer in front of them so that we can scale our API servers to handle the load
- For scaling, use the bottom-up approach of scaling

### Read Replicas

![Screenshot 2022-12-10 at 11.19.34 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fc3fcf48-1c19-4285-9a7f-0045e4fea284/Screenshot_2022-12-10_at_11.19.34_AM.png)

<aside> 💡 For most applications, read:write ratio is 99:1 (or 90:10, or 80:20)

</aside>

- If your read load is a lot and a single DB is not able to take it
- `KV-API` creates connection with `master` and one or more of the Read Replicas
- Depends on what guarantees you are giving for a given API, you can direct the API call to either master or the replica
- Deletion should happen on master, changes should be propagated to the replicas
- Beware of Replication lag between master and replica - it should be bare minimum
- Don’t randomly add Read Replicas (similar to not randomly caching)

### Sharding and Partitioning

- If your application becomes write heavy and the master is seeing a lot of writes
- Vertically scale as much as you can
- Once you’re happy with vertical scaling (can’t do anything else there), then start horizontally scaling
- We’ll talk about problems with this architecture in a later class. This is already a good place to begin with. A very standard approach to scaling.

[https://drive.google.com/file/d/1lvZCSczUInvrfuH7XMlPSW-b1XLHPyPL/preview](https://drive.google.com/file/d/1lvZCSczUInvrfuH7XMlPSW-b1XLHPyPL/preview)