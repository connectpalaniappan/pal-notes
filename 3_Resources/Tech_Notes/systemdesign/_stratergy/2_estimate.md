
1. [Estimation]()
   1. [Requests per second](#requests-per-second)
   2. [Read/write ratio]()
   3. [Storage](#storage)
   4. [Bandwidth](#bandwidth)
   5. [Length of URLs](#length-of-urls)

# Estimate
* Estimation would be required to identify how to scale the system.
* This is an optional step
  * interviewers want candidates to estimate, as part of processing the requirements.
* If you’re familiar with Fermi or market sizing questions, 
  * doing a quick back-of-the-envelope estimate shouldn’t intimidate you.

### Requests per second
* What's the initial number of users? And the expected growth?
* Number of concurrent users?
* How much data is queried per request?
  * number of writes per second?
  * number of reads per second?
  * ratio of writes to reads?
       
### Bandwidth
* How many servers are needed?
* Maximum of
  * No of active users * (images per user per day) * (number of times viewed per image) / (requests per second) (or)
  * No of active users * (images per user per day) * (number of times viewed per image) * size of the image / bandwidth

### Web socket connection
* **Each server can hold 65k (~50K) connections at max because max port is 65K**
* 20 servers can hold 1 million connections
* 200 servers can hold 10 million connections

### Storage
* How much storage will we need?
  * depends on the type of data i.e. text, image, audio, video? 
  * No of active users * (images per user per day) * size of the image * days
  * Helpful to decide whether you need to shard or add read-replicas to scale your database
    * Storage capacity is less (say 1.71 GB) and a lot of read requests, you don't need to shard.
    * Storage capacity is lot more, then it is better to shard.

### Length of URLs
* when the URL has only a-z, A-Z and 0-9, there are total 62 characters
* **URL length of 1 can support 62 unique URLs**
* length of 2 can support 62 * 62 unique URLs
* length of 6 can support 56.5 billion
* length of 7 can support 3.5 trillion

* Miscellaneous questions
  * Scalability
    * Can there be spikes in the traffic?
    * number of communication links?
    * Throughput
    * Latency
  * What network bandwidth are we expecting? 
      * manage traffic and balance load balancers. 
  * Performance
    * How to make reads and writes fast?
    * What is the expected read-to-write delay?
    * What is the expected p99 latency for read queries?
    * CPU utilization
    * Disk utilization