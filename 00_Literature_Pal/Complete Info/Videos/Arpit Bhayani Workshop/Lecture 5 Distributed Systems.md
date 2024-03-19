---
tags:
 - people/pal
 - date/2024-03-18
---
![Screenshot 2022-12-18 at 3.44.01 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d4d6f19f-8cfd-4d38-a8bc-17f78f2f2c3f/Screenshot_2022-12-18_at_3.44.01_PM.png)

- He has figured out a particular pattern that people usually follow for building distributed systems.
- Most of his learning about distributed systems comes from textbooks and working/speaking to senior engineers about how they truly built distributed systems
- Why design a load balancer? It is what makes a system distributed. While designing it, we’ll get into the nitty-gritty.

# Distributed Systems

- Without this, all the platforms which get a massive load won’t be able to handle that load.
- The beauty: Distributed Systems (DS) make multiple components split across multiple machines look like a single coherent system.
- Our aim: solve bigger problems and at scale.

<aside> 💡 The best and worst thing about distributed systems:

Everything that can go wrong will go wrong

</aside>

## Key to designing a good distributed system

- Start with a Day 0 architecture
- Scale each component

## Whys and Why Nots of Distributed Systems

### Why

- Vertical scaling has a limit (as we’ve discussed in a previous class) and hence, we need to horizontally scale.
- It also gives fault tolerance as we’re not relying on a single machine for everything. Even if one machine goes down, you’re okay.

### Why not

- We need to build `observability` to get visibility into your system as we need to monitor when a machine has gone down/if the machine is overburdened/not performing as expected.
- `Latency`: Nothing comes for free. As soon as we use DS, the only way for machine to communicate with each other is through the network, which increases latency as network is the slowest means of communication (fastest = CPU L1 cache > RAM > Disk > Network = slowest)
- Too many things to manage: but you don’t really have any option if your business requires you to use DS to handle the scale at which it is operating.

## Load Balancers (LB)

![Screenshot 2022-12-18 at 4.20.52 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6ab5e7d3-9180-4c6a-99c6-acb607ab011c/Screenshot_2022-12-18_at_4.20.52_PM.png)

- One of the most important components of any system as we keep adding it in front of anything that we want to scale and we take it for granted.
- Use case: Synchronous requests (REST API endpoints, gRPC, etc.)

### Advantages

- Fault tolerance
- No over-clocked server - LB balances the load thereby ensuring that no server is overwhelmed. It defines the balancing strategy for balancing the load across the servers.

### Load Balancing algorithms

- They answer the question: how would a LB decide which backend server (the blocks marked as API in the diagram above) to forward a given request to
- The ones discussed below are the ones practically used:
- `Round Robin`: (uniform infra, small variation in response times)
- `Weighted Round Robin`: (non-uniform infra, small variation in response times)
- Least Connections (large variation in response times)

# Design a load balancer

![Screenshot 2022-12-18 at 6.02.22 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/74c55689-37e8-4256-a81d-92f0c93ea626/Screenshot_2022-12-18_at_6.02.22_PM.png)

- tunable algorithm: We should be able to use any of the algorithms mentioned above

## Terminology

- LB Server: It is the server that is running the LB code
- Backend Server: Auth service, Profile Service, etc. - the servers in front of which we want to add the LB

![Screenshot 2022-12-18 at 6.05.46 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d587662b-0454-4e69-a68f-6b1a879e4380/Screenshot_2022-12-18_at_6.05.46_PM.png)

## Setup

The Backend Servers will have to be setup (with their own IP addresses)

The LB server should be able to take in any request as input - that needs to be set up (with its own IP address)

There has to be a mapping of which Backend Servers can the LB direct the request to.

![Screenshot 2022-12-18 at 6.10.00 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c067e566-0ba6-4d18-b091-a36be5ca52b4/Screenshot_2022-12-18_at_6.10.00_PM.png)

## Configuration

Where will the mapping/configuration be saved?

- It should be saved in a DB

What should we save in the config?

- list of backend server IP, port combinations (`backends`)
- need to store the algorithm that the LB is using (`algo`)
- any configuration that we need for the algo that we are using (`algo_config`)

### The flow till now

![Screenshot 2022-12-18 at 6.16.43 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a05875b7-f973-47d9-84e8-a3b380e59f9f/Screenshot_2022-12-18_at_6.16.43_PM.png)

![Screenshot 2022-12-18 at 6.21.35 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a4412126-658a-4953-8eab-585cd14ac4d5/Screenshot_2022-12-18_at_6.21.35_PM.png)

- We can use whatever DB we want for `config` DB

### Improving it

- But there is a problem with the flow so far (assume that `config` DB is up for 100% of the time):
- How can we keep the `config` in sync between the DB and the LB server? (e.g. some developer updated the configuration from the AWS console, the source of truth in the DB gets updated but the in-memory copy in the LB server is still stale). The two most common ways of keeping systems (any systems, not just for our LB use-case) in sync:
- Since we don’t want to make an API call from the LB to the DB, we are going to go with the Reactive approach. Thus, we can use a Realtime Pub/Sub.

## What if something goes down?

<aside> 👴🏻 Whenever you are designing a system, always think about what would happen if any of the components go down

</aside>

(for now, we’ll assume that the LB server cannot go down - we’ll make it horizontally scalable later on)

### Backend server going down

How do we detect if a backend server has gone down?

- We can set up health checks that send an event to a RPS to update the config if the health check fails.
- We need something to monitor the backend servers - this will have a heartbeat/health checks service for each of the servers, connection to the config DB so that it can update the config when a heartbeat/health check fails and connection to the RPS to which it will send an event when a heartbeat/health check fails which would push that to the LB server so that it can pull the latest config from the DB.
- We’ll call it `Orchestrator`.
- We can do an ICMP ping to each of the backend servers. However, in this case, we would only check if the server is running or not. Not whether the process on which our REST service is running (which is running on a particular port). Thus, it is possible that our REST service goes down but our server is still running. This wouldn’t catch that.
- Thus, the customer can run the REST service on any port in a server, but for each server they need to export a `/health` endpoint on a particular port (say, 8080) on a particular protocol (say, TCP) that we (the LB creators) can call to monitor if the process is running or not.
- That is why servers don’t send heartbeats to orchestrator as orchestrator itself can change. The Orchestrator uses the config DB to determine the host:port for each server and call `host:port/health` and if it receives a success status code (e.g. 200), then it determines that the server is active. Otherwise, it will mark the server as down.
- This is why, in the LB configuration, we need to also include the health check endpoint that the customer’s service has to expose.

![Screenshot 2022-12-19 at 12.51.41 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7cbca8a6-07b0-4fd0-aa31-6629c60e19dc/Screenshot_2022-12-19_at_12.51.41_AM.png)

### Monitoring the performance of Backend servers

- Not recommended to use an `Orchestrator` for this as it would put too much responsibility on the Orchestrator
- So, we can use a separate service that monitors the vitals of each server (like CPU utilisation, memory, disk, network). Typically, we use `Prometheus`.
- Prometheus is a very famous tool to monitor infra. It can be used to monitor the vitals of anything - not just an instance, but also Redis, MongoDB, and application-level stuff.
- The idea: Prometheus doesn’t want instances to send data to it. It will go and pull data from each of the instances.
- How:
- Prometheus has this vital information for every single server in your whole infra. Not just the backend servers connected to the LB. But also on the LB server and Orchestrator itself.
- Now, it is not necessary that the Orchestrator is called only if one of the servers went down. We might want to inform the Orchestrator that a particular server has been at 100% CPU utilization for the past 5 hours so that it can replace it as it is overwhelmed. How can Orchestrator get to know this? It can periodically check the DB that Prometheus is using to store the historical vitals data.

![Screenshot 2022-12-19 at 12.51.17 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bec8e0af-c3ff-4bd7-bc0d-bac8bf9239c0/Screenshot_2022-12-19_at_12.51.17_AM.png)

<aside> 🔑 Again, think about implementation at every single step. If we don’t think about implementation, we’ll just be drawing boxes. Don’t assume that you’ll just get some information. Think about how you’ll get the information that you want to get.

How are we doing it? Why are we doing it?

</aside>

### LB Server goes down

What if the LB server goes down itself?

- The entire infra crumbles as it is the point of contact.
- We can’t have it as the single point of failure.
- Thus, LB server itself is a horizontally scalable node. It looks like one LB when you create one but there are many LB servers and request can go to any of them, which is then forwarded to one of the backend servers.
- The key question: how?

The situation:

![Screenshot 2022-12-19 at 1.22.35 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/adabf69d-0ceb-4da1-804f-bd35a9a2c2c4/Screenshot_2022-12-19_at_1.22.35_AM.png)

- Although we might have said that we want 1 LB to balance the load across X Auth Service instances, AWS creates Y number of LB servers, which collectively act as one LB.
- Question: how does the routing of a request happen?
- We can use a DNS where we store a mapping of a human-recallable URL string to the IP addresses of our LB servers.
- Where is this DNS running?
- Still, how does the routing happen?

![Screenshot 2022-12-19 at 1.40.31 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/043287c0-2080-431b-8433-98877daf1803/Screenshot_2022-12-19_at_1.40.31_AM.png)

- You cannot create a TCP connection with a domain name. Only with an IP address.
- So, you have to first resolve the domain name using a DNS resolver and then, create a TCP connection with the LB whose IP address you’ve received.

<aside> 💡 Here, we have seamlessly scaled LBs and avoided making LBs a single source of failure. If one of the LB servers goes down (this can be detected by Prometheus and removed using Orchectrator), we can simply remove the IP address of that LB server from the DNS resolver’s configuration so that next time it receives a request to resolve the corresponding domain name, it will only pick from the LB servers which are active.

</aside>

## Overall flow recap

### The initial setup and how to set up the configuration

![Screenshot 2022-12-19 at 1.51.57 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/94af6afd-2550-45fa-8f09-f12ecbd521f8/Screenshot_2022-12-19_at_1.51.57_AM.png)

### How to optimise fetching the configuration

![Screenshot 2022-12-19 at 1.52.15 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a0b1d5d2-1147-4cce-a447-0a9eec64bb7a/Screenshot_2022-12-19_at_1.52.15_AM.png)

### Syncing the in-memory config with the true config

![Screenshot 2022-12-19 at 1.52.46 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9b5e20e5-0bf9-4e81-a222-2c5c9d5ca1e8/Screenshot_2022-12-19_at_1.52.46_AM.png)

![Screenshot 2022-12-19 at 1.53.51 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0dd20162-3adc-4f74-8839-76ed42c8b454/Screenshot_2022-12-19_at_1.53.51_AM.png)

### How to keep a track of the health of the LB servers and the backend servers?

![Screenshot 2022-12-19 at 1.55.32 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c70901f5-d33e-4261-96b4-f62e32a98b7b/Screenshot_2022-12-19_at_1.55.32_AM.png)

![Screenshot 2022-12-19 at 1.59.39 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6138e2d2-5a5f-4d97-a4b1-8e888da10d0c/Screenshot_2022-12-19_at_1.59.39_AM.png)

- here, the Orchestrator will check whether both the LB servers and backend servers are healthy.
- If any of the backend servers are down, the Orchestrator will update the config DB. This triggers an event in the RPS to which the LB servers are subscribed to. Thus, the LB servers get notified of the update and they pull in the latest change in the config DB into their in-memory copy.
- Instead of Redis, we can use any Realtime Pub/Sub

### How to decide how many LB servers you need?

![Screenshot 2022-12-19 at 2.01.54 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab9c250c-21a7-43fe-b55c-4275513abc1d/Screenshot_2022-12-19_at_2.01.54_AM.png)

- Suppose each LB server can handle only 10 connections and 11 connections come in.
- We’ll need to spin up another LB server.
- But what is the criterion for spinning up another LB server?
- All the infra vitals are being monitored and stored by Prometheus
- Orchestrator periodically queries Prometheus to see if LB servers need to be scaled up or not.
- If it sees that the connection limit of the current LB servers has already been exhausted:
- Orchestrator is the mastermind behind everything - it is keeping track of everything that is happening in our entire infra so that LB servers can do the bare minimum of what they are supposed to do - which is: accept the connection and forward the request.

### Scaling load balancers

![Screenshot 2022-12-19 at 2.07.10 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7a9676d2-50fc-4b21-bfab-a68c44632485/Screenshot_2022-12-19_at_2.07.10_AM.png)

- There are multiple LB servers but how would the client connect to one of them?

![Screenshot 2022-12-19 at 2.08.01 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2c503ae5-97f1-4af1-b9f4-5acc02704f1a/Screenshot_2022-12-19_at_2.08.01_AM.png)

- This brings the DNS server into the picture

## Everything Put Together

![Screenshot 2022-12-19 at 2.09.35 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9fcc326e-125d-47c0-9e13-3cf160508964/Screenshot_2022-12-19_at_2.09.35_AM.png)

- Most of the components have been explained in detail beforehand
- The new part: Autoscaling for making our system extensible
- The natural question: What if CoreDNS goes down?
- Similarly, for Orchestrator, we’ll need more machines as one machine can’t do so much. It will be a master-slave architecture (not the one that we have for Databases where there is a master node and data gets replicated to the slave nodes, for example). In this case, the slave nodes will do all the hard work of sending heartbeats, scaling up, scaling down, etc. Master will monitor everyone to ensure that they are doing their job well or not.
- All this makes up a load balancer. No single point of failure. Everything is horizontally scalable.
- LB server vs CoreDNS server
- Prometheus vs Orchestrator

# Remote locks

![Screenshot 2022-12-19 at 2.39.55 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d2b02f2a-26ab-4f32-b82e-568f96c9210d/Screenshot_2022-12-19_at_2.39.55_AM.png)

- Remote locks are anything that helps us coordinate multiple machines (e.g. Machine 1, Machine 2 and Machine 3 in the image above) together
- Why Remote? Because it is accessed over the network.

## An understanding of locks in general

![Screenshot 2022-12-19 at 11.07.55 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c74bcf88-bc9e-4ee6-a2c1-d8788fc0ed26/Screenshot_2022-12-19_at_11.07.55_PM.png)

- Threads: How do multiple threads sync? Through mutex and semaphore
- Processes:
- Similarly, the fastest shared storage between 2 machines is something that is remotely accessible, like a Remote Lock (network).

RAM, Disk, Network - 3 different levels.

<aside> 💡 This is how we should be thinking the next time we need to sync across processes or threads or machines: what is the fastest shared storage between them?

</aside>

## Understanding Remote Locks

![Screenshot 2022-12-19 at 11.18.32 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d02940a-9e2c-41d5-9ce0-041b4aae6d6b/Screenshot_2022-12-19_at_11.18.32_PM.png)

### Example

We take the example of a remote queue (hypothetical) that was written by a naive developer in a way that makes the queue unprotected.

### What does no protection mean?

- In the example above, assuming that a bunch of messages has been entered in the queue, Consumer 1 can read the first message from the queue as well as Consumer 2.
- Remember: a message queue is one where a message is read only by one consumer and then, it is deleted from the queue.
- What we need to do: Ensure that when Consumer 1 is reading the first message from the queue, Consumer 2 should not be able to read it at that instant, it should wait. We don’t care about throughput at the moment. The goal is to understand Remote Locks.
- This is a standard problem of `readers–writers`

### Setup

![Screenshot 2022-12-19 at 11.25.08 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e04f5e7-fa64-4aaf-b6de-5edf1aa366e2/Screenshot_2022-12-19_at_11.25.08_PM.png)

- Queue 7 is a remote queue
- Consumers 1, 2, and 3 are 3 separate machines
- They are accessing Queue 7 over the network.

### Solutions

- DB entry: once a consumer starts reading from the queue, make an entry in the DB indicating that the queue is locked for reading.
- What to store?
- What kind of properties are we looking for from the DB?
- Which DB gives us all of the properties above?

## Solution

![Screenshot 2022-12-20 at 12.18.04 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8526deff-67c0-4c4e-97cb-152b8041d097/Screenshot_2022-12-20_at_12.18.04_AM.png)

### Overall flow

- multiple people contending to get the lock
- only one of them should be able to acquire the lock
- Once it is done with its execution, it releases the lock
- Then, someone else from the pool of people contending to acquire the lock will get the lock
- Repeat from step 3

### The requirements from the lock manager

![Screenshot 2022-12-20 at 12.24.20 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5701a7c1-32f9-43c4-8bba-71ef963e88de/Screenshot_2022-12-20_at_12.24.20_AM.png)

- atomic operations
- automatic expiration
- Both Redis and DynamoDB meet both the requirements
- We can also use a SQL DB if we want with the TTL being implemented using a cron job.

### Implementation

- The most common implementation of this in the world is Redis (Everyone uses Redis)
    
- The way to store it: key = queue ID, value = consumer ID with expiration time. If the consumer doesn’t release the lock within that expiration time, release the lock for everyone. This means this is the maximum time for which a consumer can hold the lock.
    

![Screenshot 2022-12-20 at 12.29.39 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e02ef75a-29e3-4b5e-8695-f87752b46dae/Screenshot_2022-12-20_at_12.29.39_AM.png)

- acquiring lock
- releasing the lock

## Practical use-cases?

- MongoDB - one example but a lot of places where this is practically used
- MongoDB provides ACID guarantees and provides transactions. It is also a distributed system. Thus, there are multiple shards across which our data is distributed.
- So, when we’re doing a transaction, which is a distributed transaction in the case of MongoDB, we’re affecting some rows of one shard, some rows of another shard and so on.
- We don’t want any of these rows in any of the shards to be updated by any other transaction while the transaction above is being committed.
- Here, MongoDB uses its own implementation of a remote lock manager to do this!
- Thus, we’ll end up needing remote locks when we have a distributed transaction setup.

## Distributed Locks

- One problem in the implementation above: the Redis DB is a single point of failure
- We can’t solve it by saying that we’ll run Redis in cluster mode. When we fire a query, it will be sent to one Redis instance. Which makes the Redis instance a single point of failure (SPoF).

<aside> 💡 We look for this kind of guarantee in systems where we are okay to compromise a bit on throughput because as soon as we turn to `distributed` for anything, we are choosing to compromise on throughput. Not a huge dip but we should be okay with that.

</aside>

- This is where we use `Distributed locks`.
- Its only job: ensure that the lock manager doesn’t become a SPoF.
- Algorithm: Redlock - very famous
- The way to handle the case where a Remote Lock manager might fail is to just distribute what we did in a Remote lock.

![Screenshot 2022-12-20 at 1.30.34 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c2b13a3d-9c06-4ef3-8559-cddeb3c7b72c/Screenshot_2022-12-20_at_1.30.34_AM.png)

- get 5 independent lock managers (Redis nodes)
- Acquiring lock phase:
- It is a hectic process but you continuously keep trying to acquire the lock on a majority of the lock managers.

### Why do this?

- In this setup, even if one of the lock managers goes down, there is a consensus on who owns the lock at a given moment
- Without this, the Redis instance becomes a SPoF - if it is down, the entire system is down. This also leads to data loss if you’re running Redis in a mode where it is not persisting anything to the disk.
- As mentioned above, throughput will take a hit and you should be okay with it as it is a tradeoff.
- The beauty of this design: e.g. suppose one consumer (say, Consumer 1) acquired a lock in 3 out of 5 lock managers but then 2 of those lock managers on which it did have a lock go down, what happens?

<aside> 🔥 Please implement this to learn better!

</aside>

### When to do this?

- When the time to acquire the lock is considerably lower than the time to do the processing after you’ve acquired the lock.
- Again, won’t work for a high-throughput system. You trade throughput for inconsistency of the system.

## QnA/Discussion

- The consumers can all have IP addresses of each of the lock managers in a distributed locks setup to whom they make a request to acquire the lock. But you can also use a Proxy server in front. You can keep a track of which lock manager has gone down and update the list in each of the consumers using a real-time Pub/Sub, etc. We can keep making it as complex as we need based on our requirements.
- Instead of using Redis’s redis.nx function, we could also use a SQL DB and add a unique constraint on the key column and the starvation part can be handled by running a cron job that monitors the TTL. We can absolutely do it. There can be different implementations. Thus, focus on core properties that we need so that we can implement it on any DB that gives us that property or any variation of it.

# Bonus

Code walkthrough from 2:31:00 onwards in Lecture 6.

# Recommended Reads

- [Maglev: a fast and reliable software network load balancer](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/44824.pdf)
- [Chubby: a lock service for loosely-coupled distributed systems](https://static.googleusercontent.com/media/research.google.com/en//archive/chubby-osdi06.pdf)
- Blogs on distributed systems on [https://arpitbhayani.me/blogs/](https://arpitbhayani.me/blogs/)
- Implementations of RedLock on Github
- Blog on RedLock by Martin Klepmann
- 2 videos on implementation of distributed transactions

[https://drive.google.com/file/d/1qs5EBjm1aMT6ftzRpO_QPzCWiLWzHAqz/preview](https://drive.google.com/file/d/1qs5EBjm1aMT6ftzRpO_QPzCWiLWzHAqz/preview)