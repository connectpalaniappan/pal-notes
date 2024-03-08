## Rate-limiting

### Algorithms
* Token bucket algorithm
  * Request comes for the first time, add an entry of timestamp and number of tokens (5 tokens per minute).
  * When the consecutive request comes within the rate-limiting interval (say 1 minute), reduce the token.
    * when there are n more tokens, drop the request.
  * When the consecutive request exceeds the rate-limiting interval (say 1 minute), reset the bucket with tokens. 
* Leaky bucket algorithm
  * One side of the bucket, you add request
  * Otherside poll and process the requests
  * when the incoming requests exceed the bucket capacity, rate-limit it.
* Fixed window counter
  * For each interval, start with a zero counter
  * Increment the counter until the rate-limiting value reaches.
  * Cons: Spiky requests because a lot of requests can come at the end and beginning of a rate-limiting interval. 
* Sliding logs
  * For each user, have separate timestamps
  * discard older entries and check for the size of the queue.
  * When the size is greater than rate-limit, discard request. Otherwise, add a timestamp.
* Sliding window counters
  * Compress the user entries by having a count for each timestamp and also total requests processed in the rate-limit interval.
  * setting the size of the queue to Max Requests allowed 
  * try to remove the old entries only if max size is reached by comparing timestamp

### Problems

#### Thundering herd problem
* Blocking requests to allow requests to be processed one at a time.
  [FB live video](https://youtu.be/IO4teCbHvZw)

#### Bulkheading

#### Other Reasons
- sudden traffic from another service
- start load testing
- malicious DDOS attack
- Shared resources such as CPU, memory, disk vs network I/O could be impacted

### Server-side Solutions

#### Graceful degradation
* reject requests when a metric is not within a threshold

#### Throttling a specific client
* Request rate-limiting 429s client side way to handle server throttling
* Ensure appropriate quotas as implemented to drop requests specific to a client which is DDOS-ing.
  [Reddit insfrastructure](https://youtu.be/nUcO7n4hek4?t=1514)

#### Backpressure
TODO

#### loadshifting
TODO

#### Retry handling

### Client-side Solutions

#### Backoff policy

#### Timeouts

#### Avoid single point of failure
TODO

#### Circuit breaker
- Hystrix
- resilience4j
