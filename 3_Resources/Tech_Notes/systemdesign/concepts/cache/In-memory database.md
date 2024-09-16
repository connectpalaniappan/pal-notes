---
aliases: 
 - cache
tags:
 - resource/technology
 - resource/cache
 - resource/systemdesign
 - nexus/note_concept
---

- Purpose:: [[Fast retrieval]]
<!--SR:!2024-03-22,3,250-->
- Bottleneck:: [[Unavailability]]
- Bottleneck:: [[data loss]]
- Optimization:: [[Clustered architecture]]
### Ask whether you really need the cache?
* If you have a performance issue, can you solve it at the source? 
* What is slow? Why is it slow? Can you architect it differently to not be slow? 
* Can you prepare data to be read-optimized?
  
### If you really need the cache, then
* How do you see the values in the cache (black box vs. white box cache)?
* What happens in a cold start of your system? Can the system cope with traffic if the cache is empty?
* What is the performance penalty of using the cache?

### Problems with not using cache
- Calls to the database may take a lot more time.
- no other reliable source when the data source is down.
- **Distributed cache as the data is very large, we need to split the data and store in several caches.**

### Used in
* CDN
* server side
* client side

### Cache setup
* local in-memory cache
* local on-disk cache
* global cache
* distributed cache

### Cache invalidation
* Write-through
* Write-back
* Write-around

### Cache eviction policies 
* First In First Out (FIFO)
* Last In First Out (LIFO)
* Least Recently Used (LRU)
* Most Recently Used (MRU)
* Least Frequently Used (LFU)
* Random Replacement(RR)
  
## Examples

### Redis
### memcache


