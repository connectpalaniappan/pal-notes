---
tags:
 - people/pal
 - date/2024-03-18
---
![Screenshot 2022-12-21 at 10.40.44 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bbd40f65-2adf-4c02-bc1a-b220eff6ad3c/Screenshot_2022-12-21_at_10.40.44_PM.png)

# Foundation for ID generation

<aside> 💡 This part is not limited to ID generation. The foundation and concepts can be applied to many other use-cases

</aside>

- Why do we need IDs?
    - To uniquely identify something (e.g. object, row (RDB), document (MongoDB), event (Kafka)) (similar to how Indians have an Aadhar number, Americans have Social Security Number [SSN] to identify each person)

## Problem Statement #1

![Screenshot 2022-12-21 at 10.44.19 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/12011e1a-8223-4e2f-9f94-ebbaf6df29fb/Screenshot_2022-12-21_at_10.44.19_PM.png)

- seems like a very simple problem statement but things become complicated as we add distributed systems to it.

<aside> 📢 Disclaimer

The ID generator is not a remote service that gets called by the application server. It is a part of the application logic and resides in the same server as where we are invoking the function which is followed by storing a row (or object, etc.) with that unique ID

</aside>

- Simple setup: You need to write a normal procedural code where you are writing a function

## Approach #1: Time as ID

- Since we need something unique every time and time is always moving forward, why can’t we just use a measure of current time as the ID?
- Just return the epoch msec

![Screenshot 2022-12-21 at 10.50.22 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/14df209e-61d9-4ef1-966d-d4d4faf4d610/Screenshot_2022-12-21_at_10.50.22_PM.png)

- This is a good start and this basic assumption (that time is always moving forward) is used in a lot of systems.

### What’s the issue?

![Screenshot 2022-12-21 at 10.53.51 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a75561ab-3a21-4826-bf17-16fcbe765620/Screenshot_2022-12-21_at_10.53.51_PM.png)

- Enter: distributed systems
- This approach works fine if only one machine is involved
- However, if we have multiple machines and this function is invoked at the exact same time multiple times, then we lose the uniqueness.
- Thus, the ID generation logic is no longer globally unique, a.k.a. `Collision`!

### How can we handle collisions?

<aside> 💡 Wherever there is a tie, we add a tie-breaker.

</aside>

In our case, the tiebreaker is the machine ID. If we concatenate the machine ID with the epoch msec, it will make the ID unique (e.g. `m1-1729`)

![Screenshot 2022-12-21 at 10.56.03 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/668b56c2-b1ca-4a07-aefc-b204541fd680/Screenshot_2022-12-21_at_10.56.03_PM.png)

### What if the program has threads?

- 2 threads on the same machine can invoke that function at the exact same time leading to collision!

### How to handle that?

- Following the tie-breaker approach, we can use `thread_id` as the tiebreaker.
    
    ![Screenshot 2022-12-21 at 10.59.38 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ba44910a-c23e-4357-9618-ce16c9ba7687/Screenshot_2022-12-21_at_10.59.38_PM.png)
    

### Can we do better?

- Although this approach, after the iterations that we went through technically works, is there a different approach as well?
- The main issue with this approach is that the ID becomes too big. Do we really need to store such lengthy IDs?

## Approach #2: Using Static Counter

- We use one static counter that increments every time it is invoked (assume `counter++` is atomic, a.k.a. thread-safe to avoid writing a lot of code now [e.g. using algorithms like COMPARE and SWAP, etc.]) instead of the thread ID.
    
    ![Screenshot 2022-12-21 at 11.02.51 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f1b48194-1578-4a21-9c27-a247e438a1fd/Screenshot_2022-12-21_at_11.02.51_PM.png)
    
- A static counter is specific to a particular machine.
    
- Now, since the static counter is always moving forward every time it is invoked, time is redundant now as it is not adding anything and is just unnecessarily lengthening our ID.
    
- So, we remove time from the ID as it makes our ID leaner (smaller)
    

### Issues with Static Counter

- The counter is an in-memory variable
- What if the machine dies for some reason/reboots?
    - The counter would start from 0 and would regenerate the same IDs
    - Thus, we lose global uniqueness

### How to handle that

- Persist the value of the counter of the disk
- Next time the machine reboots, read the last value of the counter from the disk and resume from where you left off.

<aside> 💡 This is the distinction between volatile and non-volatile storage. It seems simple now to think that this is obvious. But it is important to be explicit about this. It makes us have the thought process ingrained.

</aside>

- This example is a classic case of our data being volatile and whenever we want to resume it, we have to store it in non-volatile storage. Here, the fastest non-volatile storage is the disk.

![Screenshot 2022-12-21 at 11.25.41 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/22d78838-fbff-4f6d-a452-8f6d3be93e66/Screenshot_2022-12-21_at_11.25.41_PM.png)

- This gives us fault tolerance
- The first load from the disk, increment the counter, save to disk and then return the ID.

### The issue with this?

- Every time the function is invoked, we are doing a disk I/O.
- This will significantly reduce our throughput.

### How can we reduce it?

- Approaches involving process or thread sharing would have to do message passing or communicating through the OS kernel which adds it own overhead
- The solution lies in writing to the disk periodically. However, we have been thinking about `time` whenever we think about how to define the period (e.g. every N seconds). But we can use other variables as the period too. E.g. in this case, the ticks of `counter` itself can be the period (after every 1000 increments of `counter`.

![Screenshot 2022-12-24 at 10.54.58 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9049fc32-2f53-49f1-8124-7482bf9da6dd/Screenshot_2022-12-24_at_10.54.58_AM.png)

- We have slashed disk I/O by 1000 times which is a huge improvement. The flush frequency (1000 above) can be any other value based on our appetite for how frequently we want to write to the disk.
    
- How to resume `counter` in this case if our machine crashes?
    
    - The safest value would be: load the saved value and add `flush frequency + 1` to it to avoid a `collision`.
    
    <aside> 💡 Important to think about: the value that I’m starting with, is it safe enough when the machine restarts?
    
    In this case, you would be losing out on the range of values between the last stored counter and the last stored counter + flush frequency. This is okay because the goal is to provide uniqueness. Not to exhaust every single integer value out there. Prioritize what we need: accuracy and performance trade-off for losing out on all possible values that could be used.
    
    </aside>
    

### Example walkthrough

![Screenshot 2022-12-24 at 11.01.34 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1eeb8e0c-52ae-4630-9966-4555c968d508/Screenshot_2022-12-24_at_11.01.34_AM.png)

- Suppose: flush frequency = 3
- Until, m1-06, the value got returned to the method that invoked the ID generation function and it also got saved on the disk. However, the machine crashed after generating m1-08 and returning that ID to the method invoking it.
- If we resumed from the saved value itself, it would lead to a collision.
- Thus, the safest way to resume: saved value (6) + flush frequency (3) + 1 = m1-10.

# Monotonically increasing IDs

- We modify the earlier problem statement to add another guarantee that all IDs would be monotonically increasing. Thus, if we have generated ID = 20, then ID generated would definitely be greater than 20.

### Why?

![Screenshot 2022-12-24 at 11.17.12 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/624d8af9-3ddb-4ef6-abf6-2b808daf55fd/Screenshot_2022-12-24_at_11.17.12_AM.png)

- This is a very strict requirement (e.g. we see this in DBs) but why do we need it in the first place
- Classic use case: transactions. We discussed in an earlier class about locks where we mentioned that when there are 2 concurrent transactions T1 and T2 that want to modify the same row. We said that T1 would acquire the lock first and once it has released the lock, then T2 would acquire that lock. But do we know which one came first and which one later? By the numbers 1 and 2 in T1 and T2: the transaction with the lower ID came first
    - Internally, this is how a database keeps track of which transactions came first and which came later so that it can prioritize giving locks to older transactions instead of newer ones. Each transaction is given an ID generated using some internal ID generator.
- Thus, this is needed for `conflict resolution`.

<aside> 💡 Whenever we are in a situation where we need to do conflict resolution, monotonically increasing IDs are the way to go.

</aside>

- Again, it doesn’t mean that we definitely need T1 and T2. It could be T1 and T3. As long as it is monotonically increasing, our job is done.

## Approach: Using Time

![Screenshot 2022-12-24 at 11.34.59 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d7a8d2cf-3a51-4025-bf59-6b24efa03de8/Screenshot_2022-12-24_at_11.34.59_AM.png)

- We know that time is always moving forward
- Instead of concatenating machine ID followed by time, we can do the reverse.
- In this case, time occupies the most significant bits of our ID.
- This ensures that the IDs generated would be monotonically increasing

### Example

![Screenshot 2022-12-24 at 11.36.25 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dc23b3f0-906a-4eb6-b17e-b01a9ff6b92b/Screenshot_2022-12-24_at_11.36.25_AM.png)

- one big benefit of this: it gives us rough sortability out of the box (as the one that came first will have a smaller value). This is why almost every single ID generation algorithm uses time on LHS.

### The issue with this?

- This still doesn’t guarantee strictly monotonically increasing IDs as clocks can go out of sync across machines. The clock in a machine can deviate by becoming faster or slower. Even though we blindly rely on it, it doesn’t always give us the right time.
    
- This (clock drifting) is very common in production environments.
    
- Why does a clock slow down or become faster?
    
    - In every machine (laptop, mobile phone, etc.), there is a quartz crystal that is vibrating.
    - It has a particular frequency at which it vibrates, which is constant, and it can degrade because of external factors.
    - Our computer/hardware is always counting the vibrational frequency of that crystal and once the count hits that vibrational frequency, it represents 1 msec or 1 sec (depending on the granularity of the clock)
    - Because it is a mechanical movement of the quartz crystal, it is dependent on external factors.
    - If you put the machine in a very cold environment, the vibration of the crystal would slow down a little. If you put the machine in a warm environment, the vibrations would speed up. Simple physics: if you provide more energy, it will lead to more kinetic energy, which will translate into more vibrational energy. In a very cold environment, the kinetic energy would be taken out of the system, thus the vibrational energy would be reduced and things would slow down.
    - Thus, the clock ticks become longer and the clock moves slower than the actual clock.
    - This really affects the clock of the machine. It is all physics.
    
    <aside> 📖 Read this: [https://www.newyorker.com/magazine/2018/12/10/the-friendship-that-made-google-huge](https://www.newyorker.com/magazine/2018/12/10/the-friendship-that-made-google-huge)
    
    A very interesting story of debugging relating to bit flipping where external factors can affect computer hardware
    
    </aside>
    
- Example:
    
    ![Screenshot 2022-12-24 at 12.11.18 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e08b5241-e41a-4e0a-91de-e7ec163f7930/Screenshot_2022-12-24_at_12.11.18_PM.png)
    
    - Here, machines with IDs 2, 7, and 9 have the right clock but the clock of machine with ID = 4 moves a little faster.
    - Thus, if all 4 machines are invoked at the same instant, machine 2 with generate 232 (time = 23, machine ID = 2). Similarly, machine 4 will generate 244 (24 + 4). Till here, it is monotonically increasing.
    - However, the ID generated by machine 7 will be 237. Thus, the sequence of generated IDs is no longer monotonically increasing.
- Thus, because of external factors, we cannot guarantee monotonically increasing IDs. We have to think about all this whenever we want to provide strong guarantees.
    

## Central ID Generation Service: Sneak Peek

![Screenshot 2022-12-24 at 1.24.56 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e5fd256-fa49-4bf2-a889-c08e0609ef3e/Screenshot_2022-12-24_at_1.24.56_PM.png)

- One way to solve the clock skew problem is to have a central ID generation service to which every server makes an API call.
- Earlier, the ID generation logic was on the client side. Now, it is in a centralized server.

### Pros

- Guarantees 100% monotonically increasing IDs with ease

### Cons

- This is a single point of failure (SPoF)

### How to improve

![Screenshot 2022-12-24 at 1.26.45 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/486fcac8-fb0f-4cdb-8274-7a104d788546/Screenshot_2022-12-24_at_1.26.45_PM.png)

- Use multiple ID server instances behind a load balancer.
- Now, whenever any of the instances gets a request, it has to communicate with the other ID server (s) to agree upon the last generated ID so that the current instance can generate a higher ID.
- Thus, the two (or more) servers have to continuously `gossip` to ensure that the IDs generated are monotonically increasing, with every request. Thus, throughput goes down.

### Issues with this

- From a very simple problem statement, to avoid SPoF, we have had to add multiple ID servers, and load balancers, and ensure gossip between the servers on each request (this is too frequent). This is very messy and has now become a very ugly-looking system.

## Conclusion

<aside> 💡 There is no way to distribute and guarantee strict monotonicity

</aside>

- Thus, wherever you see monotonicity as a primary criterion, you never see distributed systems. E.g. RDBs, `id` column - gives strict monotonicity - it is a single server running the exact algorithm that we’ve discussed.
- To approach this: ask if you can relax some constraint
    - For e.g. can we have non-integer IDs, do we really need strict monotonicity?
    - The first step in supporting strict monotonicity is to question why you need strict monotonicity in the first place. If it is really needed, you cannot make it distributed and it has to run on a single server.

# Central ID Generation Service - Amazon’s way

## Approach

- relax the approach of strict monotonicity but we guarantee uniqueness
    
- instead of sending just one ID on each request, the ID server sends a range of IDs that the requester owns now.
    
- In the case of Amazon, assume that there are 2 services: `orders` and `payments`. We store a counter for each of the services in the DB with an initial value = 0.
    

![Screenshot 2022-12-24 at 2.06.38 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f594ea4a-a270-4c1d-ab02-22d0275a1869/Screenshot_2022-12-24_at_2.06.38_PM.png)

## Setup

- Assume that there is a fleet of machines - one set for `orders` and another set for `payments`.
    
    ![Screenshot 2022-12-24 at 2.08.02 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b0e10599-208a-4bff-a4a4-98c8c126a7f6/Screenshot_2022-12-24_at_2.08.02_PM.png)
    
    - The API servers running the `orders` servers would be making the API call to our ID generation service.
    
    ## The flow
    
    ![Screenshot 2022-12-24 at 2.17.21 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6223e33e-2d3b-4213-86c5-0693c9498306/Screenshot_2022-12-24_at_2.17.21_PM.png)
    
    - When `Server1` starts up, it needs a set of IDs to process.
    - It will make an API call (`get_id_batch()`) to the load balancer for our ID generation service
    - The load balancer will direct the request to one of the ID generation servers.
    - The server will take an exclusive lock on the row corresponding to the service requesting a new batch of IDs (e.g. `orders`), increment the counter for that row by the number of IDs requested (e.g. 500), and return a range of IDs (e.g. [0, 500))
    - Now, `Server1` can use the range of IDs it received in any way it wants. It is better to use them in a sequential way - it will maintain an in-memory counter that keeps a track of how many IDs from the range it received has it exhausted.
    - Now, `Server1` can start serving requests to the `orders` service. It will create an order in the `orders` table using the ID stored in memory from the range it received as mentioned in the previous step.
    - Now, when `Server2` gets booted up since it doesn’t have any IDs to use, it will similarly request for a range of IDs and say, it receives [500, 1000).
    - Once the range of IDs for `Server1` is close to being exhausted, it makes another API call requesting for a fresh batch of IDs.
    - The `payments` service can do the same thing.

## DB choice

- The property that we need from the DB is atomicity.
- Thus, any DB that supports atomic transactions would work (e.g. RDB, Redis, DynamoDB)

<aside> 💡 Again, focus on the core properties that you want from your DB. The choice of the actual DB just remains a business decision.

</aside>

## Con

- It is possible that `Server1` requested 2000 IDs [0, 2000) and crashed right after receiving them. In the meanwhile, `Server2` also booted up and received 2000 more IDs [2000, 4000).
- Now, when `Server1` reboots, it makes another request for the range of IDs to use (as it was storing the range it previously received in memory, not persisting on disk). It will receive [4000, 6000).
- In this case, the ID range [0, 2000) goes unused. AND IT IS OKAY to lose out on some range as numbers are gigantic. 2^64 integers are possible. No one is going to exhaust it in the near future.

## Conclusion (tradeoffs)

- You cannot request too big of a range of IDs because if the machine requesting the range of IDs crashes, we lose out on that range. E.g. if we request for 1M IDs, we would be losing out on 1M numbers.
- We also cannot choose a very small range because, in that case, we’ll be making too frequent requests for batches of IDs.
- Thus, we have to find the sweet spot based on the number of requests you are getting on the service requesting the range of IDs.
- The ID generation service will just return `min` and `max`, not the explicit list of IDs.

## Questions

- The ID servers can be serverless functions themselves. Keep it super simple.
- A lot of concurrent requests to the DB are not going to happen by design + we are only storing one row for each service. So, we are not going to have to worry about scaling the DB.

# UUID

## What is UUID?

- a very common ID generation algorithm
- 2 variants: UUID-4, UUID-6
- It is a simple function (not a central remote service) that generates 128-bit integers (it is a huge number)
- One just needs to import the function and invoke it (no need to make any network call), and it creates an in-memory ID. Every time you invoke it, it will create a unique ID that is very likely to have not been seen before.
- The probability of ID collision with UUID is very small.

## Pros

- They do a very good job in most scenarios
- Lightweight to generate
- Easy to use
- Don’t have to worry about much (since 128-bit, enough values to last our lifetime)
- Hence, very popular
- Also, they are seemingly random. Thus, they provide good security as it is hard to guess the next UUID that would be generated.
    - This way, a hacker can’t just scrape our whole website. E.g. if you have a website where `yourwebsite.com/user/1` indicates profile page of user with ID = 1, the hacker can just write a simple scraping script where they iterate across integers and scrape the data for all the users.

## Cons

- Extremely inefficient at scale because they bloat up the index and hence, don’t index well.
    
- Refer to pre-read: how indexes make DB read faster
    
    - There, we saw that indexes store the value (of the column that we have indexes) and the row ID.
    - This is how all indexes are created (index_value, row_id). Thus, row ID is part of the index.
    - Thus, if we have a smaller row ID, the index size will be smaller, and vice versa.
    - If we use a UUID, which is a 16-byte integer, the row ID in our index would be a 16-byte column.
    - Instead, if we’d used a simple auto-increment integer, it would have taken 4 bytes.
    - Thus, our indexes are nearly 4X larger (an index that would have taken 1 GB of storage will now take 4GB of storage)
    - This will happen with all the indexes being used.
    - That is why companies don’t use UUID at scale, especially in a DB where you have to indexing.
- Why is indexes bloating up in size a problem?
    
    - If we cannot store indexes in RAM, our DB would be very slow
    - Any database leverages indexes for faster reads. Whenever the DB has to JOINs, etc. they are done on the indexes and then, the DB goes to the corresponding rows to get the data that it doesn’t already have.
    - Now, if we cannot fit our indexes in RAM, even to lookup indexes, we have to do disk I/O which becomes extremely slow.
    
    <aside> 💡 That is why, to get max perf from your DB, the RAM of the DB should at least be equal to the size of the indexes that you have. This is a very common practice.
    
    </aside>
    
    - Thus, if our index size has bloated up 4X, we’ll need a larger machine to get the same amount of performance. Using a larger machine would mean larger costs. If we don’t use a larger machine, we’ll be degrading our DB’s performance.
- The reasons above explain why companies don’t use UUIDs at scale where DB performance is imperative
    

# MongoDB Object ID

![Screenshot 2022-12-25 at 10.44.40 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d3827219-8cf4-45aa-86fa-4ab9d25a6523/Screenshot_2022-12-25_at_10.44.40_AM.png)

- Their IDs sit in-between normal integers (4 bytes) and UUIDs (16 bytes) as they are 12 bytes
- first 4 bytes to store epoch sec (time on the LHS of the string)
- next 5 bytes: random
- last 3 bytes: static counter (atomic increment, that we’ve already discussed)
- The first 4 bytes representing epoch second are important as they give MongoDB rough sortability (will be discussed more later)

# Database Ticket Servers: Flickr

- Flickr: website similar to Instagram
- Database Ticket Servers: fancy name for Central ID generation service

## Why?

![Screenshot 2022-12-25 at 11.00.05 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fceea8f6-fabd-419c-93a8-39e4712338ce/Screenshot_2022-12-25_at_11.00.05_AM.png)

- One could ask why did they need it in the first place
- The reason is that their database was sharded
- E.g. say you’ve built a blogging application like Medium and have distributed your data across different nodes. You’ve ensured that all the blog posts corresponding to one user lie on the same shard.
    - However, how will you assign an ID to each blog post?
    - You cannot use auto-increment ID because that will result in multiple posts across different shards have the same ID (post 32 by user 1 in shard 1, post 32 by user 43 in shard 43, etc.) leading to collision
- Thus, whenever your database is sharded, you need a central ID generation service

## Solution: UUID?

- Not UUID: as UUIDs index badly

<aside> 🤔 If you cannot fit your indexes in-memory, you cannot make your DB fast.

One of the first things to check during DB audit can be whether the RAM of the DB is > the index size. If not, the DB cannot perform well.

</aside>

## Solution: Central Ticket Server

- They used a central MySQL server for their ID generation
- for any post published on flickr, the ID is generated from this central ticket server

### The DB schema

![Screenshot 2022-12-25 at 11.15.50 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/989a768c-1cc0-4556-939a-c704e7c43af8/Screenshot_2022-12-25_at_11.15.50_AM.png)

- `tickets` DB
- 2 tables:
    - `id`: bigint (64-bit), autoincrement
    - `stub`: char
- Unique Key on `stub` (we’ll discuss `stub` in more detail in the next section)
- Primary Key on `id`

### The flow

- The ticket server only stores one row at a given time
- It wants to leverage the autoincrement function that RDBs already provide (no need to rewrite this part)
- To be able to use DB’s native autoincrement, we’ll need to insert a new row (that is when the autoincrement is triggered)
- One simple way: delete the existing row and re-insert it without the `id` column
- This is why we needed the `stub` column - the value in that column does not matter. We just need to pass the data for at least one column at the time of insertion and that is the only purpose which that column serves.
- The `id` that gets newly generated is returned and used further!

### Implementation

1. We can delete a row and then, re-insert it in 2 separate SQL queries as part of a single transaction but that would be extremely inefficient
2. From an earlier class, we remember that update + insert can be done in one command = upsert. Similarly, we can do DELETE + INSERT = UPSERT in one command. MySQL provides 2 functions to do so.
    
    1. `REPLACE INTO`
        
        ![Screenshot 2022-12-25 at 11.27.49 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0bb0cbe2-bb17-402a-92bf-58b02b7bb98e/Screenshot_2022-12-25_at_11.27.49_AM.png)
        
        - Steps:
            - It tries to insert a row
            - If it fails due to UNIQUE KEY constraint, delete the row
            - Insert the row
        - This is why we needed the UNIQUE KEY constraint on `stub`
        - However, it still does two steps - deletion and then, insertion.
    2. `INSERT INTO .... ON DUPLICATE KEY UPDATE ...`
        
        ![Screenshot 2022-12-25 at 11.28.02 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c352ce5d-09d2-40e1-a237-5bd3d3c98bd8/Screenshot_2022-12-25_at_11.28.02_AM.png)
        
        - Steps:
            
            - It tries to insert a row
            - If it fails due to UNIQUE KEY constraint, the UPDATE clause is executed
        - Example:
            
            ![Screenshot 2022-12-25 at 11.28.19 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ff8a9837-e39a-471f-9a77-ad5eeebe0a27/Screenshot_2022-12-25_at_11.28.19_AM.png)
            
            - here, if the value for key `a` is duplicate, it will trigger the UPDATE clause:
                
                `id = id + 1`
                
        - In this case, there is just one step.
            
    
    - `REPLACE INTO` is 32X slower than `ON DUPLICATE`

## High-level design

![Screenshot 2022-12-25 at 11.31.03 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a2857bfb-ac01-4814-ab1d-b47f1fa11526/Screenshot_2022-12-25_at_11.31.03_AM.png)

- `Server1`, `Server2`: API servers that receive API requests from the end user
- When an end user creates a new post on Flickr, one of the servers, say `Server1` receives a request for uploading a photo, it makes an API call to the ticketing MySQL server requesting for an ID. Once it receives an ID, it makes a call to the PhotosDB to store the photo.

### Issues

- The ticketing server becomes a SPoF!

### Solution

- We use multiple Ticketing servers
- But then, as we had discussed earlier, they might have to continuously gossip with each other to agree on the last generated ID, right?
- NO
- We don’t need to guarantee strict monotonicity. So, the folks at Flickr did something really smart.

![Screenshot 2022-12-25 at 11.44.43 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3d06834c-ab9c-42b3-96f8-8ee534dd087a/Screenshot_2022-12-25_at_11.44.43_AM.png)

- They added 2 ID generation servers behind a load balancer in a round robin manner such that each ID generation server would either generate an odd or an even ID.
- This is extremely smart!
- How to implement it? DBs have variables we can set to specify the offset for where the auto_increment should begin from and how much should the increment be (by default, the increment is 1)

![Screenshot 2022-12-25 at 11.46.41 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9ae752f9-8cc4-4bb2-819b-69a7b577852c/Screenshot_2022-12-25_at_11.46.41_AM.png)

👈🏻 This configuration ensured that server 1 would produce IDs 1, 3, 5, 7, …. and server 2 would produce IDs 2, 4, 8, 10, ….

### How does Fault-tolerance work now

- If a server, say `Server1` goes down, the load balancer (LB) will redirect all the requests to `Server2`. Thus, the IDs generated would all be even - 2, 4, 8, 10, ….
- Once the `Server1` is back up, the LB will again start redirecting the requests to either of the 2 servers in a Round Robin manner

### Minor inconvenience?

- Once `Server1` has gone down for a while, say the last generated ID in `Server2` became 202 by the time `Server1` comes back up.
- Thus, now, the sequence of generated IDs would look something like: 1, 204, 3, 206, 5, 208,..
- This is not very aesthetically pleasing.

### Solution

- Once `Server1` comes back up, we can reset the increment_offset for both the DBs to a safe value. E.g. max of the IDs generated so far + some buffer
- Building on the example above, it could be that the last generated ID by Server2 was 202. We can reset the offset manually for both `Server1` and `Server2` as 241 and 240 respectively.
- Again, this is done purely for aesthetic reasons. There is no performance gain that one gets from doing this.

# Snowflake: Twitter

- They didn’t build a Central ID generation service. Thus, the function invocation happens on the API server itself.
- They built something called Snowflake
    - They called it Snowflake because every single snowflake in the world is unique

## The algorithm

- It is a simple in-memory function call that creates the ID (just like MongoDB)
    
- Format: 64-bit integers (as they wanted performance as otherwise it would bloat the index)
    
    ![Screenshot 2022-12-25 at 11.55.04 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c1be20a0-d4cf-4402-b62d-46db0937f7d5/Screenshot_2022-12-25_at_11.55.04_AM.png)
    
    - first 41 bits: epoch msec (again, time on the LHS - you get rough sortability + rough monotonicity)
    - next 10 bits: machine ID
        - This restricts that we cannot have more than 2^10 API servers for a particular service
        - Because this is not a central ID generation service and the function for ID generation is run on each API server itself.
    - next 12 bits: static counter per machine
- It can be tweaked however we want but the recommendation is the above
    
- When you create a tweet on Twitter, you get a gigantic number as the tweet ID. That is a snowflake ID.
    

## High-level design

![Screenshot 2022-12-25 at 12.02.39 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c687bb9f-96bb-487f-b537-459c1b94a632/Screenshot_2022-12-25_at_12.02.39_PM.png)

- Flow:
    - a user makes a request to post a tweet
    - the request goes to one of the API servers
    - the API server that received the request makes the function call in-memory to generate the Snowflake ID
    - It uses the generate ID to make an API call to the Tweets DB
- Thus, the Tweets DB receives the ID to be associated with the tweet and doesn’t generate an ID of its own. This is a standard NoSQL approach!

## Super important feature: Rough sortability

- Since the 41bits of a snowflake ID are epoch msec, with every msec, the ID are increasing

### Very common use cases for twitter

- Process the tweets in the last 1 hour to figure out the trending topics
- Process the tweets in the last 1 hour to figure out the sentiment in the world
- Process the tweets in the last 1 hour to figure out whom’s profile it needs to be added to

### How does rough sortability help?

![Screenshot 2022-12-25 at 12.28.38 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7b885d20-6427-4e33-a673-8ae2394bfa3d/Screenshot_2022-12-25_at_12.28.38_PM.png)

- With the rough sortability that snowflake IDs provide, Twitter doesn’t have to create an index on the`created_at` column
- For each of the use cases above, we need to paginate through all the tweets as there would be a million tweets in an hour. Rough sortability gives benefits in pagination.
- How does usual pagination work in a non-Snowflake ID based DB?
- One approach is `Limit-offset based pagination`: Here, after the main part of the SQL query that specifies that rows that we want to fetch, we add `LIMIT X OFFSET Y` where `Y` represents the number of rows that have already been read and `X` represents the page size.
- The issue with limit-offset based pagination is that as we go deeper into the pages, the queries become slower. This is because, every time we run the pagination query, the DB computes all the results, then it goes through `Y` rows to skip them and then it returns the next `X` rows.
    - Thus, in the first pagination query, it would skip 0 rows and directly return the first `X` rows.
    - In the next query, it would manually skip `X` rows and then return the next `X` rows.
    - In the next one, it would manually skip through `2X` rows and then, return the next `X` rows.
- Thus, limit-offset based pagination is very inefficient.
- However, since twitter uses Snowflake, it uses something called `since_id` where it specifies the IDs that have been read uptil now. For fetching newer rows, it can simply specify that it wants IDs > `since_id`. Since the DB already has an index on the ID, this query is lightning fast and independent of how deeper one is into the pages. This is extremely efficient as it directly goes to the ID after `since_id` and gives you the number of rows that you requested for!

### Benchmarking

- Implementation for benchmarking in MongoDB: [https://arpitbhayani.me/blogs/fast-and-efficient-pagination-in-mongodb](https://arpitbhayani.me/blogs/fast-and-efficient-pagination-in-mongodb)
    - Since MongoDB also uses epoch msec for its ObjectId, we can transfer the learnings and benchmarks from MongoDB to Snowflake
- Benchmarking results: [https://arpitbhayani.me/blogs/benchmark-and-compare-pagination-approach-in-mongodb](https://arpitbhayani.me/blogs/benchmark-and-compare-pagination-approach-in-mongodb)
    - It can be seen that as one goes deeper into the limit-offset based pagination (blue line) the queries becomes shorter whereas for the `since_id` based approach, the query time remains almost constant.
        
        ![Screenshot 2022-12-25 at 12.42.24 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/228cd81a-1408-4148-a02c-aef137484c6e/Screenshot_2022-12-25_at_12.42.24_PM.png)
        

## Minor Variations

## Discord

- Also uses Snowflake with a slight variation
    - Usual definition of epoch second = start from 1st January 1970
    - Instead, they chose to define the start time for calculating epoch second as 1st second of 2015
- Why?
    - This gives them a large range of values
    - e.g. if you create a DB using the standard definition of epoch msec, you’ll lose out on ~3B numbers already!

## Sony

- They have open-sourced their Go-based implementation - called it SonyFlake

## Conclusion: Pros

![Screenshot 2022-12-25 at 12.48.38 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/94385f89-9508-43dc-b67e-c4000101408d/Screenshot_2022-12-25_at_12.48.38_PM.png)

- The Snowflake approach has enabled Twitter and other companies to scale
- No moving part: no external service, just a library and a function call
- No extra load on the DB - no autoincrement, delete, update, replace, etc.

# Snowflake: Instagram

- Instagram took Snowflake to the next level which required knowing a lot about the internals of how DB works

## Intuition

- Twitter was generating the IDs in the API server and then, sending that ID to the DB
- Why not directly generate the ID inside the DB itself?

## Setup

### Requirements

![Screenshot 2022-12-25 at 1.27.17 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/96056698-f46f-4c3d-acfa-833d8cf9ce7d/Screenshot_2022-12-25_at_1.27.17_PM.png)

- IDs needed to be sorted by time (same as Twitter)
    - pagination:
        - feed (infinite scrolling)
        - Loading the profile of a person evenly
        - also needed for fetching the feed that has happened (say) in the last 1 hour, processing it, and then storing the results
    - processing of batch data
- 64-bit IDs: for efficiency on the index
    - It reiterates how important it is to keep the indexes small

### Structure

![Screenshot 2022-12-25 at 1.30.44 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3a155df2-4666-47df-856c-395f48e7150b/Screenshot_2022-12-25_at_1.30.44_PM.png)

- Since Instagram was created in 2011, they chose the start of 2011 as the starting point for their epoch msec due to similar reasons as Discord (to get a larger range)
- Since they are generating the IDs on the DB servers themselves, instead of machine ID, they are using DB shard ID (they use a sharded DB). 13 bits ⇒ they can use up to 8192 DB shards.
- Sequence number is same as the static counter that we’ve discussed before!
- As mentioned earlier, the structure of a Snowflake ID is tweakable. Twitter used: 41:10:12, and Instagram is using 41:13:10.

### Sharded DB

![Screenshot 2022-12-25 at 1.35.23 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a1cec75-1d7a-46f4-af0f-00d53898e9f7/Screenshot_2022-12-25_at_1.35.23_PM.png)

![Screenshot 2022-12-25 at 1.38.07 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/19d42dd2-eac4-4cfb-88c2-9c0965a68a00/Screenshot_2022-12-25_at_1.38.07_PM.png)

- Logical Shards vs Physical DB servers
    - When we create a DB, we create it on some server.
    - On that server, we can create other DBs too.
    - We can have `multiple DBs` (each of the blue boxes in the image on the left) on the `same server` (the single white box on the left) which has the `same tables` (each of the white lines within each blue box) with the same schema just containing different data.
    - Each of those DB instances is called a logical shard and the server on which they are created is called a physical server.
- To shard a DB, we use multiple machines (physical servers) and on each machine, we can create multiple DBs, all having the same tables with the same schema (logical shards)
- These logical shards create a logical separation within the data.

<aside> 💡 This gives anyone the ability to scale up their database. If, say, 15 physical servers have been working just fine but now we need to add another physical server, we can just create a new physical server and move one of the logical shards to the physical server. That’s it.

</aside>

- Conclusion: Multiple DB servers, each having multiple DB instances (logical shards) with each instance having the exact same schema

## Implementation: Snowflake in the DB

- For each logical shard, this is how they would define the schema of the `photos` table
    
    ![Screenshot 2022-12-25 at 1.43.37 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3aa0aafa-5920-4670-9be7-3218d6859aef/Screenshot_2022-12-25_at_1.43.37_PM.png)
    
    - `insta5` is a logical shard (or one logical DB) (other shards include `insta1`, `insta2` … `insta8192` - 8192 shards across 15 physical servers)
    - `photos` table is present in all the logical shards with the same schema
    - `id`:
        - bigint as 64 bits
        - instead of using autoincrement as the default value they invoked a stored procedure/function `next_id()` which is invoked if we don’t provide an `id` while creating a new row
- The stored procedure
    
    ![Screenshot 2022-12-25 at 1.47.06 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3a3c2e1e-4544-4a89-958c-f7d651e30c0a/Screenshot_2022-12-25_at_1.47.06_PM.png)
    
    - `OUR result bigint` means it will output a variable result of type bigint - standard way of writing procedures and functions where `result` is the snowflake ID.
    - Declaration:
        - `epoch`: first second of 2011
        - declared variables for sequence ID, current time in msec and then, shard ID. For `insta5`, the `shard_id` is set as 5
    - Execution:
        - first 41 bits = (current epoch msec - `epoch`) left-shifted by 23 bits.
        - next 13 bits = (shard_id) left shifted by 10
        - last 10 bits = per shard sequence number
            - need atomic increments
            - every DB gives a sequence
            - The method above for calculating `seq_id` is what is done in PostgreSQL (nextval) + %% by 1024 as 10 bits = 2^10.
- This way we are literally creating Snowflake at the time of insertion into the DB!
    

## Biggest advantage

- Twitter is limited by the fact that it can have only 2^10 = 1024 API servers (as 10 bits are allocated for machine ID in their Snowflake implementation)
- But Instagram has moved that burden to the DB. So, it can use as many API servers as it wants. it is limited by 8192 DBs - which is huge and not going to be exhausted anytime soon!
- This is what made Snowflake EVEN MORE AMAZING!
- The operations inside the Stored Procedure are just bitwise operations - very lightweight
- Since it is a stored procedure, it is heavily optimized with a query plan already existing.

[https://drive.google.com/file/d/12-2RlK7Q_4XCFaDfrBtgx0lxKIjgBpLC/preview](https://drive.google.com/file/d/12-2RlK7Q_4XCFaDfrBtgx0lxKIjgBpLC/preview)