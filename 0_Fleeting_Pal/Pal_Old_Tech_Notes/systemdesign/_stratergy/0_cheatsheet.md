
## Break down the problem - First design principles
So this section is to cover how to break down a problem and build a solution bottoms-up
Question your own design by asking why?

Ask questions to break down the problem.
Build the solution bottoms-up.

## keynotes - steps to solve a problem
1. Define the problem
2. Identify any assumption
   1. [Functional Requirements](#functional-requirements)
   2. [Non-functional Requirements](#non-functional-requirements)
3. Deconstruct the problem
4. Question every assumption made
   1. [Estimation](#estimation)
5. Build from ground up
   1. [Model the API/Schema](#modeling-the-apidata)
   2. [Needs of the system](#needs-of-the-system)
6. Explore analogies
7. Solve incrementally & Combine solutions
   1. [Character to describe the system](#parameter-of-the-system)
9. Test and reiterate
   1. [Bottleneck in the system](#address-bottlenecks)
10. Communicate clearly
11. Open to revision
12. Continual learning

### Functional requirements
List one or two
1. [[User questions]] - start from the user always
   1. [Who will use the system? - Users]() - Customer, Developer, partner, reseller, third-party apps, other services
   2. [Any downstream dependencies]() - Any other system that use our system. Example, recommendation(our system) using statistics. 
   3. [Which platform]() - Browser Client, Mobile client(Android device, iOS device), Desktop client, SMS
   4. [Where is the data source for system?]() - from users, other platforms
   5. [Any upstream dependencies]() - Any other system that our system uses.
   6. [Region]() - Support Localization?
   7. [Authentication & Authorization user]()
2. [Feature questions]() - Supported functionality
   1. [User journey]() - core purpose. what to focus on?
3. [Feature ideas]() - Extended features, be specific on what content?
   1. [User/Client registration]()
   2. [CRUD content]() - posts, tweets
      1. [upload/download/view]()
      2. [Text limit]() - few characters
      3. [Text format]() - html, json, csv
      4. [Protocol supported]() - http, ftp
      5. [Customize content]() - custom URLs
      6. [Case sensitive]()
   3. [File content]()
      1. [File format]() - videos, photos, pdf
      2. [File limit]() - 1GB?
      3. [Upload/Download/view]()
      4. [Content synchronization]() - desktop, mobile clients
      5. [Client offline support]() - file editing offline
   4. [List content]() - restaurants, tweet listing
   5. [Analyze content]() - filter, sort
   6. [Search content]() - Text based search, filter based, image based, map based search
      1. Match words, word correction (Did you mean?), Type ahead suggestion
   7. [Recommend content]() - news feed, timeline, curated list
   8. [Content/User Categorization]() - Enterprise vs Individual, priority/famous vs normal, high vs low
   9. [Content Grouping]() - Video channels, User groups
   10. [Content temporary or permanent]() - URLs with expiry time
   11. [Content versioning]() - file snapshot
   12. [Content verification/reconcilation]() - verify the correctness of data between two systems
   13. [Content producers]() - Users vs external sources vs generated
   14. [Content consumers]() - Users vs systems such as analytics, machine learning
   15. [Content restriction]() - public vs private
   16. [Share content]()
       1. [Whom to share with]() - Individual, group, other platform
       2. [What content to share]() - Individual text/files, Multiple text/files i.e folders
       3. [How to share]() - Public share, private share
   17. [Content enrichment]() - tagging, commenting, review, rating, replying to tweets, subscription
   18. [Content encryption]()
   19. [Content preference]() - wishlist, likes/dislikes, favourites, watch later, views
   20. [Follow user/content]() - subscription
   21. [Filter content]() - Crawlers to exclude urls in robots.txt
   22. [Manage history or expired or unused content]() - purge, migrate vs rollup
   23. [Historical data value-add]() - priceless moments, history recap
   24. [User/activity/url tracking]() - user status tracking
   25. [User association]() - friends
   26. [Analytics]() - Recommendations, statistics, trending content, suggestions, similar content, most popular
   27. [Notification]() - push, sms, email notification
   28. Business-to-Business(B2B)
   29. [Content ownership]() - Customer vs In-house data
   30. [Software self-managed vs cloud]()

### Non-functional requirements 
Pick 3 options
1. [Availability]()
2. [Consistency]()
3. [Performance - Latency]() - Round trip time; No lags
4. [Reliability/Resiliency]() - Durability
5. [Scalability - Throughput]() - Request per second
6. [Extensibility]()
7. [Performance - Streaming delays]()
8. [Accuracy]()
9. [Cost]()
10. [Security]() - Predictable URLs, Legal, phonographic, virus, fraud, privacy
11. [Observability]() - logging, metrics,
12. [release]() - feature rollouts

### Modeling the API/data

#### Define the API model
verb describing the action with input parameter and return value
1. Parameters to pass in API
   1. **Content** - id, data, name/title, Content locale (usually in headers), description, Tags, Category, userid
   2. **Timestamp** - expiry date
   3. **User specific** - id, name, location
   4. **File** - Content plus, offset, codec, resolution, location
   5. **Query** -since_id, maxId, Maximum entries to return, sort order
2. Verbs: actions to perform something
   1. Single resource - [Get with resource id]()
   2. Multiple resources; timeline - [Get]()
   3. Create a resource - [Post]()
   4. Complete update a resource - []
   5. **delete**
   6. **link two entities**
      1. *follow* - users, tweet
   7. **upload**
   8. **search** - based on id/query
3. Business logic needed to performed as part of actions
   1. Manage resource - [Source of truth - CRUD service]()
   2. Search for needed data - [Parse/extract data]() *Use case: parse for crawler URLs*
   3. Compare results - [Verifier data]()
   4. Save characters - [Shorten data]() - *Less likely to mistype*
   5. Hide actual content - [Shorten data]()
   6. Shorten the data - [Hashing - Unique key to identify data]()
   7. Search for content - [Hashing - Unique key to identify data]()
   8. Convert to a different format - [Adapt/convert/transform/resolve data]() *Use case: domain name to ip address*, *Use case: convert from one format to another*
   9. Convert to different qualities - [Adapt/convert/transform/resolve data]() *Use case: higher to lower quality formats*
   10. Remove duplicates - [Dedupe]()
   11. Match words - [Search data]() - term frequency, inverse document frequency, Multiple words combined with AND/OR
   12. Correct words - [Search data]() - Fuzzy search
   13. Suggest words - [Search data]() - Type ahead search
   14. Not show wrong content to users - [Filter data]() - *Use case: Legal issues, privacy, Hate*
   15. Avoid black-listed content based on user/external vendor requirements - [Filter data]() *Use case: web crawler to not crawl content based on robot.txt*
   16. Show relevant data first - [Order/sort/rank/prioritize data]() - *Use case: Newsfeed to show relevant feeds*
   17. Unique sequence number for a resource - [Sequencing]()
   18. Message ordering for each client in real-time - [Sequencing]()
   19. Combine data to create clusters - [Grouping]() - *group users into roles to assign permission*, *group resource for easier search*
   20. Combine results from a service - [Aggregate]() - *Newsfeed, Historical data, Sharded data*, *Not a good idea to combine chunked files*
   21. Break down into smaller chunk for easier processing - [Split data]() Scatter/Gather pattern, Divide and Conquer
   22. Send data to different user groups - [Routing]()
   23. Send data to different nodes of a service - [Routing]() - *Use case: Route to the same node with an external connection to avoid multiple connection*
   24. Expired data - [Clean up]()

### Define the data model
Nouns describing the object
1. [Entities]() - Customer, Developer, partner, reseller
   1. Litmus test for entity: If two instances of the same object have different attribute values, but same identity value, are they the same entity
   2. Same context, different use - split the entities. Example: BankingAccount, PayeeAccount
   3. Same term, different meaning - split the entities. Example: LoginAccount, BankingAccount
   4. Example: Order
2. [Value Objects]() - Immutable, lookup, static objects. E.g. paint bucket
   1. Example: Postal codes
3. [Aggregates]() - Single representation of a multiple entities e.g. merchant and their customers.
   1. Aggregates can be stored as documents/values in a document store or key-value datastore.
   2. Example: Historical, connection, real-time feeds, file metadata
4. [Associations]()
5. [Common fields]()
   1. **Content specific** -id, userId, data, name/title, Content locale, description, Category
   2. **User specific** -id, name, email, date of birth, address, phone, last login
   3. **Timestamp** - deletedTime, createdTime, modifiedTime
   4. **File** - size, thumbnail, LocationLatitude, LocationLongitude, Path
   5. **Content preference** - like count, dislike count, view count

### Estimation
Any idea or do I need to calculate()?
1. [CAP Theorem]()
   1. [Consistency]()
      1. Single primary, sharded database
   2. [Availability]()
      1. Read replicas, CQRS
2. [General]()
   1. [Number of users]()
      1. **Example**: 10 Million users
      2. **Low** - Monolith
      2. **High(>1 Million users)** - Microservice
   2. [Number of Daily active users DAU]() - Calculate read vs write requests per second
      1. **Formulae**: % of total number of users
      2. **Example**: 10% of 10 million users = 1 Million users per day
   3. [Read/Write ratio]()
      1. **Example**: 1:9
   4. [Number of users per desktop client]() - synchronization
3. [Scalability]()
   1. [Throughput]()
      1. **Formulae**: Active user * total number of requests per user per day / 86400 seconds
      2. **Example**: 1 Million user * 100 requests per day per user / 86400 seconds = 1200 requests per second
      3. **Low** - SQL/NoSQL Database
      4. **High(>10K RPS)** - Non-Blocking IO, Client Buffering/Batching requests
   2. [Read throughput: Number of read requests per second]()
   3. [Write throughput: Number of write requests per second]()
   4. [Read query throughput: How much data is queried per second]()
      1. **High(>500 TPS)** - Cache, Indexes, Materialized view, Read replicas
      2. **Very High(>1K TPS)** - CQRS,  Valet pattern
   5. [Write transaction throughput: How much data is written per second]()
      1. **High(>1K TPS)** - Sharding, multiple primary, Columnar datastore
      2. **Very High(>5K TPS)** - CQRS
   6. [Data storage limits]()
      1. **Formulae**: Number of active users * Number of write requests per user per day(10%) * bytes per request * 5 years
      2. **Example**: 1 Million * 10 * 500 bytes * 365 * 5 years  = 9125,000 million bytes = 9125 GB = 9 TB
      3. **Low** - Single primary database
      4. **High(> 4TB)** - Sharding (Same data), functional decomposition(Different data)
   7. [Cache storage limits]()
      1. **Formulae**: 20% * Number of users * Number of read requests per day * bytes per request
      2. **Example**: 0.2 * 1 Million * 90 * 500 bytes = 9000 million bytes = 9 GB
      3. **Low**: Single cache instance
      4. **High(>256GB)**: Partition
   8. [Traffic]()
      1. **Steady** - Auto-scaling
      2. **Spikes** - Pre-compute capacity
4. [Performance]()
   1. [Latency]() - for what?
      1. **Low(<200ms)**: Websocket connection(Push), CQRS
      3. **High**: Request-response, Client Buffering/Batching, Long polling(Pull)
   2. [Read Latency: Time it takes to read a resource]()
      1. **Low(<200ms)**: CDN, Cache, Pre-computation, Indexes, Materialized view, CQRS, valet pattern
      2. **High**: On-the-fly computation
   3. [Write latency: Time it takes to write a resource]()
      1. **Low(<200ms)**:
      2. **High**:
   4. [Maximum file size]()
      1. **Low**:
      2. **High(>1MB)**: Break into smaller chunks
   5. [Read/Write storage lag]()
      1. **Zero**: One database, sharding
      2. **Low(few seconds)**: Read replicas,
      3. **High**:
   6. [Stream processing delay]()
      1. **Low(few seconds)**: Stream processing
      2. **High(>hours)**: Batch processing
5. [Reliability]()
   1. [Availability]()
      1. **No** - Single database
      2. **Yes** - Load Balancer, Primary/Secondary application, Replicated databases, Leaderless replication
   2. [Durability]()
      1. **No** - Cache with no persistence
      2. **Okay** - Database
      3. **Strong** - writes to all replicas
6. [Cost]()
   1. [Minimize the cost of development]()
      1. **open source**
   2. [Minimize the cost of maintainance]()
      1. **cloud managed solution**
7. Request - Write, reads, concurrent requests, latency
8. Compute - Throughput
9. [Threads]() - Active, total, Rejected executions
10. [Request]() - Success rate, error rate,

### Needs of the system
Solve the problem - left to right
1. User needs a way to access the system - [Client]()
   1. Immovable device - [Stationary android device]()
   2. Friendly movable device - [Tablets]()
   3. Need to use everytime - [Mobile]()
   4. [Website]()
2. [Edge services]()
   1. [DNS]()
   2. Route to services - [APIGateway]()
   3. Route to servers - [Load Balancer]() 
3. Business logic processing - [Service]()
4. Fast retrieval - [Cache]()
5. Persistent storage - [Database]() 
6. Eventual consistent is fine - [Streaming]()
7. Long running tasks - [Streaming]()
8. Heavy computation query - [Streaming]()
9. [Batching]()
10. [Analytics]()
11. Miscellaneous
    1. [Deployment](#deployment)

### Parameters of the business
1. Source of truth - CRUD data
   1. [What are different ways to delete the data]()
      1. Compliance concerns - [Hard delete]()
      2. Future reference - [soft delete]()
   2. Parse/extract data
      1. [Different format to parse]()
      2. [Ways to parse]()
         1. Easier to find the answer at the top - [Breath first search]()
         2. Parent and child are independent - [Breath first search]()
         3. Child needs to associated with parent - [Depth first search]()
         4. Much easier to find the result in a child - [Depth first search]()
2. Validate data
3. Verifier/reconciliation data
   1. [Ways to verify data integrity]()
      1. Just mentioned there is a difference - [Hashing]()
      2. Need to find the difference - [Field by field comparison]()
      3. Faster way to find difference - [hashing different; then field by field comparison]()
4. Shorten data
   1. [How to shorten data]()
      1. Ok to drop characters - [Dropping characters]() - **Conflicts**
      2. Consistent result - [Hashing]() - **Conflicts**
5. Unique key to identify data - Hashing
   1. [How are unique keys generated]()
      1. Custom - [User chooses the key]()
      2. Increasing atomic number - [Unique sequence number]() - *Disadvantage: Risk of predicting the next resource id by external users*
      3. Based on data - [Unique hash keys]()
      4. Independent of data - [Unique id - uuid]()
   2. [Hashing algorithms]()
      1. **MD5** - Obsolete; Generate 128 bit (21 character)
      2. **SHA-2**
      3. **SHA-256**
      4. **CRC32**
      5. **Bcrypt**
      6. **xxHash**
      7. **RipeMD**
   3. [Minimum characters to generate unique key]()
      1. **text characters** - Each character can represent 64 variations
         1. *six character* = 64^6 = ~68.7 billion possible strings
         2. *seven character* = 64^7 = ~281 trillion possible strings
      2. **Bits** - Each bit can represent 2 variations
         1. *30 bits* = 2^30 = 1.07 billion
         2. *10 bits* = 2^10 = 1024
6. Adapt/convert/transform/resolve data
   1. [Text encoding algorithm]()
      1. **Base64** - (A-Z, a-z, 0-9, -, .) - Only alphanumeric characters;
      2. **Base36** - (a-z ,0-9)
   2. [Image encoding format]()
      1. **Thumbnail**
   3. [Video encoding format]()
      1. **mp4**
   4. [Video quality format]()
      1. **1080px**
      2. **720px**
7. Dedupe data
   1. [When to dedupe]()
      1. In requests - [Different/Same users send the duplicate data]()
      2. Duplicate data - [System has two changes 1. existing data 2. changed data]()
   2. [How to dedupe]()
      1. Simple check for duplicates - [Generate 64-bit checksum - Hashing]()
      2. [Bloom filter]() - **False positives i.e. expected result: Not a duplicate, Actual result: Duplicate;Can be reduced by building a bigger bit vector**, *No false negatives i.e. expected and actual result: Duplicate*, *Probabilistic data structure for set membership testing that may yield false positives*, *Large bit vector represents the set*, *Element is added to the set by computing ‘n’ hash functions of the element and setting the corresponding bits*, *An element is deemed to be in the set if the bits at all ‘n’ of the element’s hash locations are set*,
      3. Identify the difference - [Field by field comparison]() - **Too slow**, **Space overhead**
   3. [What actions to take when you find a duplicate content]()
      1. [Throw an error]()
      2. [Skip the content and return existing content]()
      3. [Overwrite existing content]() - *Update useful when the duplicate content is of higher quality*
   4. [Dedupe algorithms]()
      1. [Block Matching]()
      2. [Phase correlation]()
8. Search data
   1. [What attributes to search for]()
      1. [uuid]()
      2. [hashing]()
      3. [data specific attributes such as user name]()
   2. [Steps to execute search query]()
      1. [Fetch/Send the query]()
      2. [Read the data based on the query]()
      3. [Filter the data]()
      4. [Rank/order the data]()
      5. [send the data]()
9. Query data
   1. [Where would queries be used]()
      1. [Query params in API requests]()
      2. [Query params for search]()
   2. [What are the different operations supported in query]()
      1. logical expressions - [AND, OR, NOT]()
10. Filter data
    1. [What are ways to restrict/filter data]()
       1. URLs - [Based on domain, prefix, protocol]()
11. Order/sort/ranking/prioritize data
    1. [How to order data]()
       1. Latest first - [Chronological order]() - *Recent; timestamp based; epoch timestamp*
       2. Oldest data - [Reverse chronological order]() - *After last sync timestamp*
       3. [Based on the user needs]()
       4. [Relevant first]()
       5. [Most liked first]()
       6. [Client criteria based on how they want to view]()
       7. [Random]()
    2. [What criteria to rank data]()
       1. User data - [Personalization]() - first preference; *User location, language, demographic, personal history, historical searches, social graph distance, relevance, popularity*
       2. Default - [Sequence number]()
    3. [How to fetch the next set of ordered items]()
       1. [Offset-based pagination]() - **Doesn't scale for huge offset as database would fetch offset + limit rows everytime**, **duplicate reads when there writes are made at high frequency**
       2. [Cursor-based pagination based on modifiedTime or resourceId]() - *Scales well for huge data set*, *Pagination window stabilized*
12. Sequence data
    1. [How does the data need to be sequenced]()
       1. [Single node sequencer]() - **Single point of failure**
       2. Parallelism not needed - [two node with even and odd sequence]() - *Not able to increase parallelism*
       3. Parallelism needed - [epoch timestamp + machine id + sequence no]() - *Optimization: Reset sequence number every second; lesser bits to store sequence number*
13. Group data
14. Aggregate data
    1. [How do you perform aggregations on the data]() - *Use case: Update frequencies of search terms in every Trie node*
       1. Aggregate results everytime - [Aggregate all the data with equal weightage]() *Use case: Re-aggregate all the search terms everytime*
       2. Update the difference - [Aggregate all the data with different weights. Weight difference added periodically]() - **Not possible to give more weightage to the latest data**, *Use case: Keep track and update the aggregated difference in a Trie*
       3. More weightage to the latest data - [Exponential Moving Average(EMA) to add more weightage to the latest data]()
15. Split data
16. Route data
    1. [What information should we route on]()
       1. [Event type]()
       2. [Priority]()
       3. [Time]()
       4. [ResourceId]() where resource could be clientId, url
    2. [What is the strategy for routing](7_bottleneck&tradeoffs.md#service-routing---based-on-what-should-we-split-data)
       1. [Hash function]()
       2. [Route mapping to a node/service]()
       3. [Random]()
17. Branch data based on decisions
18. Cleaning historical or expired data
    1. [How do we cleanup]()
       1. [Purge and re-use unique keys]()
       2. [Migrate to another data store]() - say cassandra
       3. [rollup data]() - aggregate and store at a lower granularity
       4. [Soft-delete expired data and later perform above actions]()
    2. [When is the expiry time set]()
       1. Use does not need the data - [User deletes]()
       2. Delete historical data - [System sets a default one]()
       3. Based on user criticality - [System sets based on user]()
19. Fetcher/Receiver/Sender: Fetch/receive/send content from/to client or external vendors

### Parameter of the system
1. [Client](#client-decomposition)
   1. Purpose of client
      1. Content upload 
         1. [How to update backend](7_bottleneck&tradeoffs.md#client-push-vs-pull-vs-both)
            1. Immediate - **Push from client to server** - request/response, batch feeds, websocket
            2. When needed - **Pull from server to client**
               1. *Use case: web crawler to pull from external web servers to download content*
            3. **Hybrid**
         2. [Identify the communication protocol]() - Implement in modular way for extensibility
            1. **HTTP**
            2. **FTP**
      2. Content download - Web, Mobile, Desktop 
         1. [When to receive content from/to client/external vendors](7_bottleneck&tradeoffs.md#client-sync-updates-immediately-or-on-demand-or-both)
            1. [Request made synchronously or foreground]() - **Disadvantage: blocked on request, when user requests?**, *Use case: mobile/browser: foreground*
            3. [Requests made asynchronously or background]() - *Use case: desktop: background*, *Advantage: not blocked on request, downloading data well-ahead*
            4. Data not urgent - [Wait for update from the server]() - **Consistency issue**
            5. Data urgent - [Poll the system for latest updates]() - *Use case: Pull the current status of all users in an online app*
      3. Processing/Computation
      4. Notification from backend
      5. File chunker - File chunk and re-construct from smaller chunks
         1. [who should be chunking the file]()
            1. **Client should chunk**
               1. *Advantage: Easier to send smaller chunk*
            2. **Server should chunk**
               1. *Disadvantage: Client uploading the entire file*
            3. **Client should chunk and server should chunk it further**
               1. *Advantage: Easier for clients with lower bandwidth*
               2. *Disadvantage: Need to track updates on multiple chunk*
         2. [What basis do we determine the chunk size]()
            1. **Space utilization based on supported client** - Mobile has less space
            2. **Input/output operations per second** - frames per second
            3. **Network bandwidth**
            4. **Average file size in storage**
         3. [What should the chunk size be](7_bottleneck&tradeoffs.md#client-chunk-size-large-or-small)
            1. **Fixed chunk size** - Say 4 MB
            2. **Adaptive chunk size**
      6. Content watcher - track for any changes in local content, update indexer
      7. Content indexer - easier to search
   2. Local storage
      1. [What should we store locally]()
         1. metadata - file location, hash, size, version
         2. actual files
      2. [who would update the local storage]()
         1. Engine can manage all data
         2. Component could manage their specific data
         3. Indexer can index and manage the local storage
   3. Communication
      1. Client to client
2. [Service](#model-components)
   1. Purpose
      1. Who would perform the task
         1. Custom - [user]()
         2. Offload work to client - [client]() - **conflicts - add client id/region**
         3. At the edge layer - [Load balancer]()
         4. Pre-processing possible - [Dedicated service]()
         5. Processed when the request arrives - [Service which receives the request]() - *Separate service which would pre-generate sequencing keys*
         6. [On-prem]()
         7. [SaaS platform]()
         8. Safer to in every place the request ends up - [Client and server]()
      3. When to perform the task
         1. Task independent of the request - [Pre-process the task]() - *Pre-generate sequencing key; ranking algorithm*
         2. Immediate processing of task during write - [Immediately perform the task]() - **Latency issues; Re-generate sequencing key; Throw error after some tries**, **What would happen when there are multiple concurrent requests**
         3. Task can be performed after write - [Post processing of the task]()
         4. Task can be performed during read - [Post processing of the task]() - **Storing data until task is completed**, **Need to manage the data when requested**, *Low latency*
      4. [Pre-processing: When should the task be executed]()
         1. No pressure on existing traffic - [Scheduled at regular intervals]()
         2. Pressure on existing traffic - [Scheduled when traffic is low]()
      5. [Pre-processing: How much data needed to perform the task]()
         1. Less data - [All the data]()
         2. Huge data can be categorized by timeline - [Limit the data]() - *Use case: Order new data from the last ordered timestamp*, *Use case: Status of all whatsapp members a user sees*
   2. Network
      1. External calls from client to server and vice-versa
         1. Client needs data immediately - [Synchronous (Client pull/in-process)]()
            1. Guaranteed delivery - [TCP]()
            2. Data loss ok - [UDP]()
            4. Request/Response - [API server]()
            5. Minimal Real-time updates - [Short polling]() - **Empty requests might be high**, **New data might not show up immediately; wasting bandwidth**, **Server to track pending messages for heavy computations**, *Easier to implement*
            6. Smaller polling connections - [Long polling]() - **CPU intensive**, **Hot users would get frequent updates blocking others**, **Not easily scalable as sending to everyone is a huge load**, *New data available immediately*, *Easier to open a new connection when a connection break*, *Server does not need to track pending messages*
            7. Real-time connection to send bidirectional - [Websocket connections]() - **CPU intensive**, **Hot users would get frequent updates blocking others**, **Not easily scalable as sending to everyone is a huge load**, *New data available immediately*, *Easier to open a new connection when a connection break*, *Server does not need to track pending messages*
         2. Server sends data to single client - [Server Push]() - **Pushing to all clients leads to huge load**, *Pre-generate data to save on load* 
            1. When?
               1. immediately - [when available]()
               2. Not needed immediately - [with a delay]()
               3. Optimize based on client behavior - [Send when client is online]()
            2. How?
               1. One off requests - [Webhooks](), [Callbacks]()
               2. Real-time connection to send server events - [Send server events]()
               3. Real-time connection to send/receive bidirectional - [websocket connections]()
         3. Server sends data to multiple clients 
            1. Consistent result - [One client at a time and on failure, retry the next client]() - *Use case: Identifying the next available driver* 
            2. Pick any client - [broadcast at the same time, pick the first client which acknowledges]()
            3. Send to all clients - [Broadcast to all users when the user comes online]() - *Use case: In text-messaging app*
         4. Hybrid  
            1. All workloads on-demand - [Server pushes at certain frequency and client pulls whenever there is a need]()
            2. Huge workloads on-demand - [Pull for huge workloads and push for smaller ones]() - *On-demand for huge workloads*, *increase interaction for smaller ones*
      2. Internal calls from service to another service (Inter service communication)
         1. Send/Receive data in real-time - [Synchronous (Pull/in-process)]()
            1. Guaranteed delivery - [TCP]()
            2. Data loss ok - [UDP]()
            3. Request/Response - [API server]()
         3. Send/Receive data with a delay - [Asynchronous (Push/Pull)]()
            1. Within the same service - [Async call executed by a thread]()
            2. Decoupled - [Streaming]()
      3. Common for all communication
         1. [Identify the communication protocol]() - Implement in modular way for extensibility
            1. **HTTP**
         2. [Identify the message format]() 
            1. text 
            2. binary
            3. **Mime types** - HTML page, video, image
   3. Compute
      1. How?
         1. Only one request at a time - [Serial execution]()
         2. No dependency among request - [Parallel execution]()
         3. Dependency among request - [Concurrent execution]()
      2. Who?
         1. Stateless service - [Any node/pod in the service]()
         2. Stateful service - [Specific node/pod determined by a parameter]()
   4. Storage
      1. How to process the storing
         1. Immediately - [Synchronous request in the same thread]()
         2. Eventually with loss of data - [Asynchronous request in different thread]() - *minimum latency*
      2. State of the data
         1. No persistence
            1. Loss in saving - [Data in local memory/storage]() - impedes scalability
         2. Persistence
            1. Transactional use case - [App -> storage (Same thread)]()
            2. Read by downstream service  - [Message stream]()
            3. Transaction use case and read by downstream service - [App -> Database and App -> Message stream]() - *lag*, *in-consistency*
            4. Prioritize downstream service over transactional updates - [App -> Message stream -> Database]()
            5. Prioritize transaction updates over downstream service - [Change data capture (CDC) App -> Database -> Message stream]() - 
   5. Memory
      1. How to fetch data
         1. In real-time - [Fetch when needed using a request]()
         2. Downloading well-ahead - [Pre-fetch via event-driven]() - *Decouple sender and receiver*
         3. Downloading well-ahead, not available then in real-time - [Hybrid - fetch when needed and re-use on subsequent requests]()
      2. Where to store the fetched/computed data
         1. Need immediately - [Application memory]() - **Node failure leading to data loss**
         2. To be processed later - [Separate queue]() - *Reduces memory*
3. [Service discovery]()
   1. [Client side discovery]()
   2. [Service proxy discovery]()
4. [Database]() 
   1. Storage
      1. Persistence - [Database]()
      2. No persistence - [Application memory/cache/message stream]()
   2. Database choice - Where to store the data
      1. Custom data structure such as Trie, priority queue - [Application Memory]()
      2. Almost fixed schema + Atomic operations(ACID) + Integrity checks(Consistency) - [SQL]()
      3. Easy to extend schema + No integrity checks - [Document data store]()
      4. Read Intensive + Atomicity + TTL - [Key-value data store + caches]()
      5. Write-Intensive + Pagination 
         1. Sync processing: [Wide-column data store]() - Cassandra, HBase, Bigtable
         2. Async processing: [Message queues]()
      6. Analytics - [Columnar data store]() - Bigquery, Redshift
      7. Time series data - [Time series DB]() (Columnar data store)
      8. Graph relationships - [Graph database]()
      9. Unstructured files or static content - [Object storage]()
      10. Global data delivery - [CDN]()
      11. Search engine - [Text search database; Elastic search](), [Trie]()
      12. Default choice - [SQL]()
5. [Cache](#cache) 
   1. Update 
      1. Cache takes care of read from database - [read through]()
      2. Cache takes of write to database - [Write through]()
      3. Application updates cache on cache miss - [Cache aside]()
      4. Cache updated ahead to reduce latency - [refresh ahead]()
      5. Database updated periodically from cache - [write behind]()
   2. Invalidation
   3. Eviction - Least recently used, Least frequently used
   4. TTL - seconds, minutes, days, weeks, months
6. [Streaming](#messaging-components)
   1. Where would you place the queue
      1. Between two services - []()
      2. Between a client and a service - [Valet pattern]()
   2. Do we need persistence?
      1. Re-process message - [Temporary]() - *Default 7 days*
      2. Client is offline - [Temporary]() - *Default 7 days*
      3. Enquire anytime in future - [Permanent - Event sourcing]()
      4. Not needed - [No persistence]()
   3. How many subscribers?
   4. Streaming options
      1. Multiple subscriber + Continuous stream of messages with delays + persistence - [Event stream]() - Kafka, Kinesis
      2. Every subscriber nodes + Real-time delivery + no persistence - [Pub sub]() - Redis pub/sub
      3. Single subscriber + persistence - [Message queue]() - SQS, RabbitMQ
      4. Multiple subscriber + no persistence - [Message notification]() - SNS
      5. Spiky stream of messages, no persistence - SNS + SQS
   5. [How many queue/partition to create](7_bottleneck&tradeoffs.md#messaging-partition-the-queue-or-not)
      1. [One queue with multiple services/clients subscriptions]()
      2. [One queue with separate partition for each services/clients]()
      3. [Separate queue for each service/client]()
   6. Publishers
      1. Where would you get the messages to publish
         1. Transactional outbox [Push: Application writing to queue](4_articulatethepattern.md#transactional-outbox)
         2. Change data capture - [Pull: Reading from database logs](4_articulatethepattern.md#transactional-log-tailing)
         3. Transaction logs - [Pull: Reading from database logs](4_articulatethepattern.md#transactional-log-tailing)
         4. Polling publisher - [Pull: Client polling publisher](4_articulatethepattern.md#polling-publisher)
      2. How would you publish the messages
      3. What strategy can be used to determine which partition/queue to sent to
         1. [Send to the same partition]()
         2. [Hash of a relevant data]()
         3. [Based on priority]()
         4. [Based on group]()
      4. Who would publish the message
      5. Which messages to publish
         1. [All messages]()
      6. When would you publish a message
         1. [Immediately]()
         2. [Based on the schedule]()
      7. How to push the messages
         1. [Individual message]()
         2. [Batch of messages]()
   7. Consumer
      1. Where would write the message your read
         1. Combine, write data to a database/message queue - [Write ahead logging, Denormalizer component](4_articulatethepattern.md#write-ahead-logging)  - user vs device events
         2. Combine, Call service via API - [Gateway component](4_articulatethepattern.md#gateway-service)
         3. Use events in the consumed service 
      2. How would you consume the messages
         1. [Push messages to consumer]() - Redis
         2. [Pull/poll messages from consumer]() - Event stream, Message queue
      3. Who would consume the message
         1. [Single consumer]()
         2. [Multiple consumer with single-thread]()
         3. [Multiple consumer with multiple-thread]()
      4. Which messages to consume 
         1. [All topics]()
         2. [Based on wildcard matching topics]()
         3. [Based on message filter in a topic]()
      5. When would you consume the messages
         1. [As soon as possible]()
      6. How to commit the consumed message
         1. [Individual message]()
         2. Throughput issues - [Group messages]()
      7. Dedupe for the consumer to be idempotent
         1. No dedupe logic - [Exactly once is tough to achieve]()
         2. Dedupe possible - [Atleast once]()
7. [Batching](#batching)
8. [Edge services](#handle-external-requests)
   1. [APIGateway]()
      1. Placed before load balancer
      2. Purpose
         1. Cross-cutting concern i.e. authentication/authorization
   2. [Load balancer]() - High availability, performance and throughput
      1. Load balancing algorithms
         1. Uniform infrastructure - [Round robin]() - Distribute the load iteratively
         2. Non-uniform infrastructure - [Weighted round-robin]() - Distribute the load iteratively as per weights
         3. Response times have big variations - [Least connections]() - Pick server with least connections
         4. Websocket connection - [Least connection]()
         5. Latency sensitive service - [Least response time]()
         6. stateful service - [Hash based]()
      2. Routing to multiple load balancer - [DNS resolution]()
      4. [Where to place load balancer]()
         1. **Between Clients and Application servers**
         2. **Between Application Servers and database servers**
         3. **Between Application Servers and Cache servers**
      5. [Need to see the request or not](7_bottleneck&tradeoffs.md#load-balancers-single-vs-multiple)
         1. **Layer 4 load balancer** - No need to parse request
         2. **Layer 7 load balancer** - Need to parse request
      6. [How to perform health checks]() - Health checks monitoring
         1. **Ping servers to determine they are alive**
         2. **Servers periodically send health updates**
         3. Heartbeat(alive) vs Health check(healthy)
      7. [Loadbalancer setup](7_bottleneck&tradeoffs.md#load-balancers-software-vs-hardware)
         1. **Hardware load balancer**
         2. **Software load balancer**
   3. [DNS]()
      1. Single vs multiple domains
         1. Huge traffic vs security concerns - [Multiple DNS]()
         2. No concerns - [Single DNS]()
      2. Routing algorithms
         1. [Round robin]()
         2. [Weighted round-robin]()
      3. DNS IP address updates
         1. No frequent changes - [Manual update]()
         2. Frequent changes - [Automatic by another service]()
   4. [CDN]()
      1. Invalidation - Surrogate keys
      2. TTL - Pre-configured vs origin server response

### Bottlenecks of the business
1. Source of truth - CRUD operations
2. Parse/extract data
   1. Self referenced content 
      1. [Dedupe]() - *Use case: symbolic link within a file system can create a cycle*
   2. Infinite parsing 
      1. [Limit parsing of related content]() - *Use case: People have written traps that dynamically generate an infinite web of documents*
3. Validate data
4. Verifier/reconciliation data
5. Shorten data
6. Unique key to identify data - Hashing
   1. Handle conflicts
      1. Simple - [Add sequence number]() - **overflow with increasing sequence number, reset sequence number before overflow**
      2. Use data - [Add userId or shardId]() - **user not logged in**
      3. With user help - [Custom prefixes from user]() - *Let user choose uniqueness key*
      4. Retry - [Re-generate the conflicting data]() - *Re-generate URL short code for conflicting users*
      5. Retry with minor tweaks - [Remove, add, swap some characters]()
      6. Hashing - [Use multiple hash algorithms to generate code]()
7. Adapt/convert/transform/resolve data
   1. Data already encoded
      1. Complete - [All data encoded]()
      2. Partial - [Some parts of the data encoded]()
      3. None - [None of the data encoded]()
8. Dedupe data
9. Search data
10. Query data
    1. [Do we need to support varied characters in search query]() - uppercase? charset?
       1. [Not support varied characters]() *Simpler use case*
       2. [Support case-sensitivity i.e. upper case]()
11. Filter data
12. Order/sort/ranking/prioritize data
13. Sequence data
    1. [What happens when there is gap in the sequenced data]()
14. Group data
15. Aggregate data
    1. [How to optimize pre-aggregation]()
       1. [Reducing the amount of data aggregated based on current timestamp]() - *Use case: Aggregate drivers for a user*
       2. [Reducing the amount of data aggregated after the last aggregated timestamp]() *Use case: Newsfeed generation after a certain timestamp*
       3. [Reducing the number of user data is aggregated for]() - *Users who are recently active; LRU*, *Users based on their usage patterns*
    2. [How to save storage cost]()
       1. [Limiting the number of aggregating data]() *Use case: Based on the user usage pattern of newsfeed, we can limit to 100 instead of 250 feeds*
       2. [Delete old generated feeds offline]()
16. Split data
17. Route data
18. Branch data based on decisions
19. Cleaning historical or expired data
    1. [Race condition: Request for historical/expired data before cleanup]()
       1. [Return error and lazy cleanup later-on]()
       2. [Perform cleaning strategies and return error]()
20. Fetcher/Receiver: Fetch/receive content from/to client or external vendors


### Bottlenecks of the system
Right to left 
1. [Database - SQL]()
   1. Network
      1. Limited connections/sockets
         1. Write intensive 
            1. Data can be sharded - [Sharding]() 
            2. Lags are acceptable - [CQRS with reader/writer swap]()
            3. Non-critical writes - [Asynchronous bulk writes i.e. queue, then database]()
         2. Read intensive 
            1. Duplicate requests - [Dedupe]()
            2. Stale data ok - [Read replicas]()
         3. Equal reads/writes - [Load balancer/Proxy]()
      2. Connection time-out
         1. Critical request - [App retries]()
         2. Non critical request - [Drop the request]()
      3. Node failure
         1. in single region
            1. Primary failure
               1. stand-by present - [promote standby as primary]() - Waste of standby resources
               2. replicas present - [promote replica as primary]()
               3. multiple primaries - [redirect requests to primary]()
               4. automatic promotion - [leader election]()
                  1. Configuration server (Zookeeper, Consul) needs to let clients know about the new leader.
            2. Replica failure 
               1. multiple replicas - [load balance to other replicas]()
               3. primary can handle load - [fallback to primary]()
            3. Both primary and replica fails
               1. Backup available - [Fetch the last snapshot from the backup]()
               2. Data from another source - [Re-built the data]() - Takes time, not able to serve traffic
               3. Data can be build from intermediate data structure - [Service to maintain the data structure]()
                  1. *Use case: Indexer service which would have a reverse index to build the index e.g. reverse index with index as key and tweet ids as value*
         2. in multiple region with multiple primaries
            1. on primary - [promote replica as primary]()
            2. on primary with region outage - [fallback to secondary region primary]() - user latency could increase when the regio  is far-off
            3. on replicas - [fallback to primary]()
            4. on replicas with region outage - [fallback to secondary region primary]()
      4. Huge number of connections/Thundering herd
      5. Reduce network calls to database
         1. Reads
            1. Static data - [Application memory - In-memory cache]() - Data needs to be updated in persistence layer, all application server cache
         2. Writes
            1. batched? - [Batch writes to database]()
   2. Compute
      1. Query time/time-out/High latency
         1. Write intensive
            1. Has relation and integrity checks - [Multiple primary]()
            2. No relation or integrity checks - [Wide-Column database]()
            3. Specific functionality writes are huge - [Vertical partition]()
         2. Read intensive
            1. Bad query - [Optimize query]() 
               1. Use case - same values in IN query
            2. Full table scan for less than 20% rows
               1. Index does not exist - [create or use existing index](#index) - Writes slow
               2. Stale data is fine - [Cache]()
            3. Delete locking table - [Prefer gap locks for huge deletes]()
            4. Data retrieval is huge
               1. No index on the filter columns - [add or utilize index]() - Writes slow
               2. index exists - [Pagination by index]()
            5. Complex joins with lag - [Materialized views]()
            6. Complex joins with no lag - [Denormalized data]()
            7. Data can be purged - [Purging/Archiving the data]()
            8. Long-running analytics query - [Delegate & respond]()
            9. High volume users - [Separate database i.e. move out of multi-tenant database]()
            10. Cross-join queries -
                1. Shard key was wrong - [Better shard key]()
                2. Aggregation - [Global index to find shard]()
            11. Duplicate requests - [Dedupe]()
      2. High CPU for database node/Low throughput for application
         1. Write intensive
            1. Can be sharded - [sharding]()
            2. Non-critical writes -[Asynchronous write i.e. queue, then database]()
         2. Read intensive/Read on every request
            1. Near-static data - [Application memory]()
            2. No cache - [Cache]()
            3. No read replicas - [Read replicas](#primary-secondary-replication)
            4. Read replicas exhausted - [Horizontal scaling on replicas](#horizontal-scaling)
            5. Due to another request reading table with historical data - [Purge the historical data]()
            4. Due to another request - [Decompose the functionality]()
         3. Equal reads/writes - [CQRS]()
         4. Replication 
            1. Synchronous - [Asynchronous]()
         5. Primary over-loaded
            1. Read requests - [Node redirects to another replica]() - Multiple re-directions, High latency
            2. Read requests with load balancer - [Load balance to other replicas]() - Consistency issue
         6. Replica over-loaded
         7. Mitigate - [Vertical scaling]()
      3. Thundering herd/Huge number of queries
         1. Multiple queries to same table (N+1 problem) - [Single query to same table]()
         2. Due to cache not storing invalid keys - [Null for invalid keys](), [Bloom filter]()
   3. Memory
      1. High memory -  [Pre-compute]()
         1. When reads are huge - [Read replicas]()
         2. Due to another request reading table with historical data - [Purge the historical data]()
         3. Due to another request - [Decompose the functionality]()
         4. Aggregation - [Limit the data needed]()
            1. *Use case: Based on the user usage pattern of newsfeed, we can limit to 100 instead of 250 feeds*
         5. Mitigate - [Vertical scaling]()
      2. Concurrency issue
         1. Multiple statements executed separately - [Transaction block to ensure atomicity]()
         2. Holding a lock in a transaction block for a long time - [Reduce the lock hold time]()
         3. Isolation levels
      4. Consistency issue due to stale data
         1. In materialized view - [Denormalized data]()
         2. In replication lags
            1. No replication lag - [Synchronous write to primary & replica]()
            2. Few minutes not tolerable - [Fallback to primary]()
            3. Few minutes tolerable - [Query sent to replica]()
         3. Concerning for user? - [short-lived and user would see only for few millisecond]()
         4. Verify inconsistency - [Merkle tree]()
         5. Sync replica after they are come back online - [Anti-entrophy protocol]()
   4. Storage/Disk
      1. High storage
         1. Specific functionality - [Vertical partition]()
         2. Data not providing value - [No need to store]()
         3. Data not providing value already stored or expired - [Remove or move data out of primary]()
         4. Old data not needed - [delete unused data]()
         5. Due to indexes - [Remove unused indexes]()
         6. Overall - [Sharding](#sharding)
      2. Disk crash
         1. [Write-ahead logging]()
      3. Data loss
         1. No backup - [Checkpointing: Backup snapshots at regular intervals]()
         2. Delay in backup - []()
         3. Delay in replication - [Synchronous writes to a replica]() - Increase in latency
         4. Partial written rows - [Checksum for data integrity]()
         5. Accidental hard delete - [Soft delete preferred]()
         6. Accidental delete by a user - [Restore from Immutable backup]()
      4. Data corruption
         1. [Error correcting codes]()
   5. Scale
   6. Reliability
   7. Cost
   8. Security
2. [Database - Document store]()
   1. Network
   2. Compute
      1. Query time/time-out
         1. Indexing is slow in Elastic search - [Avoid as transaction db]()
   3. Memory
      1. Concurrency issue
         1. Conflict on MongoDB document update - [Distributed lock on documents across shard]()
   4. Storage/Disk
   5. Scale
   6. Reliability
   7. Cost
   8. Security
3. [Database - Columnar store - Analytics]()
   1. Network
   2. Compute
      1. Query time/time-out
         1. Transactional queries - [Only analytics queries]()
   3. Memory
   4. Storage/Disk
   5. Scale
   6. Reliability
   7. Cost
   8. Security
4. [Database - Wide-column store]()
   1. Network
   2. Compute
      1.
   3. Memory
      1. Consistency issue due to stale data
         1. concerning for user? - [short-lived and user would see only for few milliseconds]()
         2. replication concern - [three-phase writes]()
   4. Storage/Disk
   5. Scale
   6. Reliability
   7. Cost
   8. Security
5. [Database - graph]()
   1. Network
   2. Compute
      1. Query time/time-out
         1. Iterative queries - [Only graph algorithms]()
   3. Memory
   4. Storage/Disk
   5. Scale
   6. Reliability
   7. Cost
   8. Security
6. [Database - graph]() 
   1. Network
      1. 
   2. Compute
      1. High latency - [CDN]() 
   3. Memory
   4. Storage/Disk
   5. Cost
   6. Security
7. [Cache]()
   1. Network
      1. Limited connections/sockets
         1. Read Intensive
         2. Write Intensive
            1. Check for duplicates - [Auxiliary cache instance]()
      2. Connection time-out 
         1. Secondary instance available - [Fallback to secondary]()
         2. Secondary instance not available - [Fallback to database]()
      3. Reduce network calls
         1. Multiple network calls - [Lua script]()
   2. Compute
      2. High CPU/Latency increase
         1. On cache miss - [Refresh ahead cache]()
         2. Data reference in cache - [Store data too in cache]() - inconsistent result, increased storage space
         3. Long polling for changes - [Listener for cache changes]()
         4. Database updates followed by cache invalidation - [Write back cache]()
      3. Thundering herd
         1. 
   3. Memory
      1. Concurrency issues
         1. single statement - [Atomic instruction; Guaranteed safe]()
         2. Multiple statements - [Transaction treated as atomic operation]()
      2. Consistency issue due to stale data
         1. cache aside pattern - [Write through cache](), [Refresh ahead cache]()
         2. local cache - [Remote cache]()
      3. Save space
         1. Duplicate data - [Dedupe]()
   4. Storage/Disk
      1. High storage
         1. Huge metadata - [Store only data reference]()
         2. Non-expiring keys - [Set TTL]()
         3. No space in a node - [sharding]() 
   5. Scale
   6. Reliability
   6. Cost
   7. Security
8. [Batching]()
   1. Network
   2. Compute
   3. Memory
   4. Storage/Disk
   5. Scale
   6. Reliability
   7. Cost
   8. Security
9. [Pub/sub]()
   1. Network
   2. Compute
   3. Memory
      1. Message send to a subscriber who publishes it - [Redis support not to resend back]()
   4. Storage/Disk
      1. Multiple channel on redis - [Combine channel based on a common criteria]()
   5. Scale
   6. Reliability
   6. Cost
   7. Security
10. [Streaming]()
    1. General
       1. Lag - [Synchronous calls to database/service]()
       2. No persistence - [Streaming (Kafka)]()
    2. Network
       1. Connection overhead
          1. SQS - [Kafka has connection pooling]()
       2. Connection timeout on streaming nodes 
          1. messages are independent of consumer and data - [Load balancer to shift the messages to available node]() 
          2. message are dependent on the data - [fallback to closest available replicated node]() - **Avoid two master problem**
       3. Connection timeout for publisher
          1. Simple message - [Re-publish the message]()
          2. Huge file in message - [Separate file from message - Claim check pattern](4_articulatethepattern.md#claim-check-pattern)
          3. for consumer - [Re-read message until the message is not committed]()
       4. Reduce network calls overhead
          1. batch reads? - [Poll for messages in batches]()
    3. Compute
       1. Low throughput
          1. Due to publisher
             1. SQS - [Kafka has high write throughput]()
          2. Due to subscriber
             1. less consumers, more partitions  - [Scale consumers]()
             2. more consumers, less partitions - [Increase kafka partitions]()
       2. Errors
          1. Message failure - [Dead-letter queue]()
          2. Consumer failure - [Messages not committed and retried]()
       3. Duplicate messages
          1. Idempotency - [Consumer de-dupes]()
       3. Ordering
          1. not possible - [Order within a partition in Kafka]()
    4. Memory
       1. Concurrency issues
          1. Due to consumer reads - [Kafka ensures messages of a partition are sent to same consumer]()
    5. Storage/Disk
       1. High storage
          1. Messages can be deleted - [Fine tune deletion policy]()
    6. Scale
    7. Reliability
    8. Cost
    9. Security
11. [Application service]()
    1. Network
       1. Connection time-out
          1. Request failure - [Client retries]()
          3. Critical functionality impacted - [Highly available service]()
       2. Node failure
          1. Request node failure - [fallback on available node]()
          2. Compute node failure - [Leader election among workers]()
          3. Region failure - [fallback to another region]()
       3. Huge number of connections/Thundering herd
          1. One node - [Multiple nodes + Load balancer]()
          2. Increase in regular traffic - [Auto scaling]()
          3. Spike in regular traffic - [Pre-compute capacity]()
          4. Specific/critical functionality - [Separate service]()
          5. Low priority requests with retry - [Rate-limit to drop]()
          6. Low priority requests with no retry - [Rate-limit to process later]()
       4. Avoid network overhead
          1. Calls to other components - [Valet pattern i.e. direct calls to components say S3]()
          2. Call to clients - [Websocket connection]()
          3. Call to another service - [Persistent TCP connection]()
       5. Concurrency issue at network level - remote lock
          1. Redis lock (Redlock)
             1. Single KV node available - [Pessimistic locking: Lock object in KV store with (key, value) -> (resource, consumer_id)]() - Node failure; Lock incorrectness
                1. lock held infinitely - [TTL to expire lock]()
             2. Multiple KV node available - [Acquire > 50% remote lock on multiple nodes]() - High contention; Not ideal for high-throughput systems
          2. Two-phase lock
          3. SAGA lock
    3. Compute
       1. Request time-out/High latency
          1. Read requests
             1. On the fly computation
                1. Synchronous - [Pre-compute and store in cache]()
                2. Asynchronous - [Pre-compute and store in memory store]()
             2. Repeated requests - [Cache data/computation]() - **Increased storage space**, **Inconsistent results**, *Use case: Store top suggestion for each trie node along with the node value*
             3. Repeated computation - [Cache computation]() - *Use case: Convert domain name to ip address*
             4. High probability of next page request - [Pre-load request data in cache]() - **Increased storage space**, *Use case: Search auto-fill pre-order results based on the top suggestion*, **Not possible to order in another dimension**
             5. Write throttling - [Only writing at certain intervals]()
             6. Possible to index data for faster retrieval - [Only indexing at certain intervals]() - *Use case: Update trie in application memory after a certain interval*
             7. On serving almost static data/images
                1. CDN not available - [CDN]()
                2. CDN not an option - [Load balancer Cache]()
                3. Load cache not available - [Cache]() - Redis/Memcache
             8. More connection needs to be established - [Long polling]() - **CPU intensive**
             10. More connection needs to be established - [Websocket connection]() - **CPU intensive**, *Save some time in establishing connection*
             11. 
          2. Write request
             1. Synchronous operations after database update - [Change data capture (CDC) from database for asynchronous operations]()
          3. Any request
             1. Specific/critical functionality - [Separate service]()
       2. High CPU/Low throughput
          1. Read requests
             1. Client makes compute intensive requests - [Decentralized computation on client]()
             2. Client makes a lot of requests 
                1. Synchronous - [Client buffering/batching in application memory]()
                2. Asynchronous - [Buffering/batching in message queue]()
             3. Long polling - [Short polling]()
             4. [Non-blocking IO]()
          2. Write requests
             1. Calls to other components - [Valet pattern i.e. direct calls to components say S3]()
          3. Any requests
             1. Specific/critical functionality - [Separate service]()
             2. New feature - [Rolling updates]()
             3. New feature with complete rollout (bad) - [rollback]()
          5. Mitigate
             1. Stateful server - [Vertical scaling]()
             2. Stateless server - [Horizontal scaling]()
       3. Thundering herd/Huge number of requests
          1. One node - [Multiple nodes + Load balancer]()
          2. Limited request queue size - [Separate queue for high priority requests]()
          3. Specific functionality - [Separate service]()
          4. Updates are frequently pushed (e.g. monitoring) - [Pull updates from dependent service]()
       4. Errors
          1. Retry or not
             1. Retry possible - [Retry the operation]()
             2. Retry not possible - [Send the error to the client/service]()
          2. Error not consistent - [Idempotent errors]() - *Same error code and message always*
    4. Memory
       1. Out of memory/High memory
          1. Due to data
             1. Aggregation
                1. Huge data aggregation - [Limit data to aggregate]()
                   1. Based on current timestamp - *Use case: Aggregate drivers for a user*
                   2. Based on last timestamp - *Use case: Newsfeed generation after a certain timestamp*
                   3. Based on active users
                   4. Based on user patterns
                2. Query across shards - [Global index on sharded data]()
             2. Cyclic reference in data - [Avoid or limit cyclic reference]()
             3. Duplicate data - [dedupe]()
          2. Due to requests
             1. Low priority requests - [Load shed]()
          3. Mitigate - [Vertical scaling](), [Horizontal scaling]()
       2. Concurrency issue for threads - share same memory
          1. Single service - Concurrency issue
             1. When race conditions occur i.e. How conflicts happen
                1. [read then write]()
             2. Strategy to handle conflicts
                1. Conflicts are limited - [Optimistic locking/Last update check during commit]() 
                2. Conflicts are high - [Pessimistic locking/2 phase commit]() - Latency issues in acquiring the lock
                3. [Mutex]()
                4. [Semaphores]()
                5. [Lock free]()
             3. How to resolve conflicts when detected
                1. [First write wins]()
                2. [Last write wins]()
                3. [User resolving conflicts]()
             4. After conflicts happen, how to handle failures
                1. [Retry the current transaction]()
                2. [Rollback all the previous transaction]()
                3. [Compensating the failed current transaction]()
                4. [Throw error for user to resolve manually]()
          2. Multiple service - Concurrency issue
             1. When race conditions occur i.e. How conflicts happen
                1. [Request for expired data before cleanup]()
                   1. [Return error and lazy cleanup later-on]()
                   2. [Perform cleaning strategies and return error]()
             2. When would conflict resolution happen
                1. Handled in same service - [single service/node, single region writes]()
                2. Conflict avoided + Strong consistency - [2 phase commit]()
                3. Conflict detected/eventually fixed + Eventual consistency - [SAGA pattern]()
                   1. Who would handle conflict resolution
                      1. Coupled Transaction co-ordination with managed global retries - [Orchestrator or reconciler or scheduler-agent-supervisor pattern]()
                      2. Decoupled Transaction co-ordination with no global retries - [Choreography]()
                   2. Who would play the role of orchestrator
                      1. [Client]() - Conflict resolution is not easy for multiple clients
                      2. [Server]()
       3. [Consistency issue](7_bottleneck&tradeoffs.md#service-handle-race-conditions)
          1. Write to multiple components - [Write in the same transaction]()
          2. Database/cache update to application memory
             1. Update instantly for a sticky node - [Write through application memory]()
             2. Pull on demand - [TTL to expire application memory cache]() - **Latency increase**, **hits to database at the same time**
             3. Pull aggressively - [Periodically poll database for updates]() - **Eventual consistency issue**
             4. Push updates from [Push: Redis pub-sub - Change data capture to push database updates]() - Near real-time updates
             5. Hybrid pull and push - [Pull & Push: Redis pub-sub primary and corrective action by periodically polling database]()
          3. Update from other services
             1. Pull from other service - [Increase pull frequency]() 
                1. Increases load on other services
             2. Push from other service - [Use redis real-time pub-sub]()
    5. Storage/Disk
       1. High storage
          1. File storage - [Object storage]()
          2. Mitigate - [Vertical scaling](), [Horizontal scaling]()
       2. Concurrency issue for processes - shared same disk
       3. Errors
          1. Accidental deletion - [Recover from backup]
    6. Scale
    7. Reliability
    8. Cost 
       1. Low CPU usage across compute resources - [Compute resource consolidation pattern](4_articulatethepattern.md#compute-resource-consolidation-pattern) - **not easily scalable** 
    9. Security
12. [Websocket/Server send evernts service]() - Only for real-time communication
    1. Network
       1. Connection time-out/failure
          1. Pending messages - [Pulls messages from application server based on last connect timestamp]()
          2. Offline clients - [Drop messages when they are not critical]()
          3. Offline clients - [Server retry after exponential backoff]()
          4. Offline clients - [Clients can take a compensating action]() *Retry after exponential backoff*
          5. Offline clients - [Inform user to take compensating action]() *Retry their action*
          6. Offline clients - [Push notification to get the user online]() **Users need to opt-in for device or browser push notification**
       2. Huge number of websocket connections
          1. Due to internal connections
             1. Server mesh to every other server - [Replace with redis dedicated channels which server subscribes to]()
          2. Due to external connections - [Auto scale]()
    2. Compute
       1. High CPU
          1. Query on database for every message to identify which node to route to
             1. destination user on same node - [Send directly]()
             2. destination user on different node - [Send to redis pub-sub which is subscribed by destination node]()
          2. Users connections on random nodes - [Smart service to redirect client on which server subscribes to]()
          3. Business logic - [Move processing to a different service]()
       2. Error
          1. Messages dropped
             1. Manual correction - [Users triggers manual update from application server]()
             2. Automatic - [Long polling application server]()
    3. Memory
    4. Storage/Disk
    5. Scale
    6. Reliability
    7. Cost
    8. Security
13. [Load balancers/Proxy server]()
    1. Network
       1. Connection time-out
          1. Request failure - [Load balancer (maybe hardware) to redirect request to available node]()
       2. Node failure
          1. One load balancer node - [Configure multiple load balancer]()
          2. Primary fails - [Configure secondary as primary]()
       3. Huge number of connections/Thundering herd
          1. Increase in regular traffic - [Auto scaling]()
          2. Spike in regular traffic - [Pre-compute capacity]()
    2. Compute
       1. Request time-out/High latency
          1. Mitigate - [Increase timeout config for backend servers]()
          2. On serving static data - [CDN]()
       2. High CPU/Low throughput
       3. Thundering herd/Huge number of requests
          1. Within capacity - [Queue requests]() 
             1. Slow processing of requests
    3. Memory
    4. Storage/Disk
    5. Scale
    6. Reliability
    7. Cost
    8. Security
14. [CDN]()
    1. Network
    2. Compute
       1. High latency
          1. Specific geographical location - [Setup CDN node closer to a geographical location]()
       3. High number of requests
          1. Viral content - [Shield/Multi-layer CDN i.e. CDN btn CDN and origin server]()
    3. Memory
       1. Consistency issue
          1. Cache invalidation
    4. Storage/Disk
    5. Scale
    6. Reliability
    7. Cost
    8. Security
15. [DNS]()
    1. Network
       1. Node failure
          1. Multiple nodes - [Leader election algorithm]()
    2. Compute
    3. Memory
    4. Storage/Disk
    5. Scale
    6. Reliability
    7. Cost
    8. Security
16. [Client]()
    1. Network
       1. Connection not available when calling a service (Availability)
          1. Node dies - [Failover to another server]() - **Extremely difficult**
          2. Redundant service available - [Fallback to redundant service]()
          3. Trivial processing - [Offline processing]()
          4. Critical processing by server - [Timeout]()
          5. Critical processing by server - [Circuit breaker]()
          6. To update backend Listener for local storage changes - [Asynchronously update backend]()
       2. Slow network/Network congestion (Reliability)
          1. Download
             1. File chunk high resolution - [Download lower quality]()
             2. Non-critical data - [Stick to Critical data]()
          2. Upload 
             1. File chunks
                1. Server tracks - [Request from server for failed chunk]() - complexity in identifying the client to send the request
                2. Client tracks - [Client resends failed chunk]() - timeout, lot more chunk might be sent
             2. Data from local storage
                1. Client tracks - [Client to send from the last checkpoint]()
          3. Both
             1. Existing websocket connection - [Perform health check and reconnect]()
       3. Huge connections/Thundering herd
          1. Data is pulled from server by polling - [Webhooks to push data from server]() - Lesser inconsistency issues
          2. Data cannot be pushed from server - [Long polling by client]() - Lesser inconsistency issues
          3. Long polling has multiple connections - [Websocket connection]() - Lesser inconsistency issues
          4. Long polling/websocket not possible - [Poll parallel requests within allowed limit]() - Inconsistency issues
          5. Parallel requests not possible - [Sequential requests]() - Low throughput
          6. Multiple websocket connection from client/vendor - [One websocket connection per client/vendor]()
       4. Huge network bandwidth
          1. Download every content
             1. What user needs - [On-demand download]()
             2. Persistence available - [store in local]()
          2. Upload to server
             1. Not dependent on backend - [Local processing]()
             2. Search request on first keystroke - [Wait for user to enter minimal characters for search]()
             3. Post all updates - [Post only when user clicks submit button]()
             4. Frequent updates - [Buffer and send after certain interval]()
             5. Duplicate requests - [Dedupe; Client can cancel previous ones]()
             6. Huge file upload - [Chunk the file]()
          3. Retry on failures
             1. Retry on huge file upload failure - [Retry on smaller chunks]()
             2. Send all updates - [Implement proper checkpointing to restart from a point of failure]()
          4. Connecting with server - [Peer to peer communication among clients]()
             1. Security concern - [Check with server for valid clients]()
             2. Identifying with client to connect - [Ask server for client information]()
             3. Inconsistency among clients - [Send updates among clients]()
             4. Crash of local storage - [Sync with server or multiple clients for data]() 
    2. Compute
       1. Request time-out
          1. Processing on server takes time - [Local processing/indexing]()
          2. Slow requests - [Buffer the requests]()
       2. High latency on average
          1. Download
             1. Huge data response - [Paginate the request]()
             2. Receiving unneeded data - [GraphQL; Send only client requested data]() - *Reduce the number of network trips*
             3. [Long polling]()
             4. Huge connection time - [Websocket connection]() - **Complicated setup**, *Save some time in establishing connection*
          2. Upload
             1. Sending all updates - [Send only differential updates]()
             2. Sending all info - [Send only critical info]()
             3. Multiple requests - [Batch the requests]()
             4. Non critical requests - [Async requests to backend]()
             5. Huge connection time - [Websocket connection]() - **Complicated setup**, *Save some time in establishing connection*
       3. High latency on the tail end
       4. High CPU/Low throughput
          1. Processing all data - [Process differential updates]()
          2. Fetch everytime from server - [Pre-fetch data from the server to save future requests from client]()
          3. Compute intensive - [Store results from the past/history]() - *Recent history have a high rate of being reused*
          4. Multiple requests to server - [One request from client and merge results; Frontend for backend (Composition) pattern, APIGateway pattern]() 
       5. Thundering herd/Huge number of requests
          1. Parallel requests to get data - [Sequential requests]() **decreases the throughput**; *use case: For a web crawler not to overload external web service, threads can send requests by placing those in an in-memory queue* 
          2. Parallel requests to get data - [Buffer the remaining requests]() 
          3. Call to get same data - [Metadata caching]()
    3. Memory
       1. Concurrency issue
       2. Consistency issue
          1. With server 
             1. Simple conflicts - [Automatic resolution on server]()
             2. Complicated conflicts - [Manual user resolution]()
             3. Hybrid approach of the above
          2. With other components (indexer) in clients - [Listen to changes in local storage]()
          2. With other clients - [Listen to changes in other clients]()
    4. Storage/Disk
       1. Space restriction
          1. Only what user needs - [On-demand download and delete everything else]()
          2. User intervention - [Inform user to delete unneeded files from desktop]()
          3. Duplicate data with multiple apps - [Mobile: Build super apps]()
          4. File chunks 
             1. when users don't rollback often - [Only the latest chunk]()
       3. Disk crash
       4. Data loss
          1. Users turn off the device/logs off
             1. Device - [Persistent storage]()
       5. Data corruption
    5. Scale
    6. Reliability
    7. Cost
       1. Low CPU usage across compute resources - [Compute resource consolidation pattern](4_articulatethepattern.md#compute-resource-consolidation-pattern) - **not easily scalable**
    8. Security

### Streaming - Messaging components
Move transaction data to messaging queue
3. [Event processing strategy]()
   1. Strategy
      1. [Process and filter events](4_articulatethepattern.md#pipe-filter-pattern) - Pipe and filter pattern
      2. [Combine events to de-dupe](4_articulatethepattern.md#aggregator-pattern) - Aggregator pattern
      3. [Split events to different queues/partitions/consumers](4_articulatethepattern.md#routing-pattern) - Router pattern
      4. [Sequential: Process related messages in order](4_articulatethepattern.md#sequential-convoy-pattern) - Sequential Convoy pattern - split to ensure sequence
      5. [Prioritize messages](4_articulatethepattern.md#priority-queue-pattern) - priority queue
         1. [Priority queue: preempt or continue processing a low priority message when a high priority message arrives]()
         2. [Upgrade message priority dynamically or not]()
      6. [Asynchronously process request/response](4_articulatethepattern.md#requestresponse-pattern)
   2. Processing bottleneck
      1. [How to optimize processing stateful events such as connection, shard]()
         1. **Stream processing: Requests from queue/other service to client can be routed to the same node based on the hash of the something**
         2. **Batch/Stream processing: Message needs to be published to the same partition/queue based on the partition key which would be based on the hash of something**
      2. [How to avoid duplicate messages](7_bottleneck&tradeoffs.md#messaging-queue-messages-that-can-be-duplicated)
         1. **Checking for duplicates on the consumer side**
      3. [Messages that end up in failure](7_bottleneck&tradeoffs.md#messaging-queue-messages-that-end-up-in-failure)
         1. **Write to retry queue**
         2. **Drop**
      4. [Messages that can't be processed](7_bottleneck&tradeoffs.md#messaging-queue-messages-that-cant-be-processed)
         1. **Dead-letter queue**
         2. **Drop**
      5. [Throughput issues]()
         1. **Group messages**
      6. [Queue cluster goes down](7_bottleneck&tradeoffs.md#messaging-when-the-entire-queue-cluster-is-not-available)

### Batching
1. Configurable parameters
   1. [when do you need to batch]()
      1. **Batch & write**
      2. **Aggregation of data greater than few minutes**

### Database
1. Configurable parameters
   1. [How to find the right database]()
      1. Addressed in keynotes
   2. [Which data do we persist]()
      1. **Data which needs to be re-used**
      2. **Store the checkpoint/snapshot data to recover from crashes**
   3. [Which data we should persist]()
      1. **Data used for in-memory computation and is not re-used**
   4. [How to persist data]()
      1. **Application memory: Write snapshot to disk**
      2. **Enable persistence for cache. Not enabled by default**
      3. **Event sourcing: Queue are persisted for a limited period**
      4. **Persistence by default for other storage options**
   5. [Who would own the storage]()
      1. **Single service**
      2. **Multiple services**
         1. *Disadvantage: Schema updates need to be handled in multiple service* -  Anti-pattern for SQL/NoSQL databases
   6. [How to write to the single/multiple storage]()
      1. **Application would make a synchronous request to multiple storage in atomic operation**
      2. **Application would make an asynchronous request to multiple storage in atomic operation**
      3. **Application would make an asynchronous request to each storage separately**
2. Bottleneck
   1. [Ways to optimize reads]()
      1. SQL
         1. **Materialized view to split reads and writes** [](4_articulatethepattern.md#materialized-view) - read performance, pre-computed
         2. **Cleanup historical/expired data**
      2. NoSQL
         1. **Store data in the way it is going to be queried**
      3. Storage reads
         1. **Bigtable(Cache) to store multiple files in one block** 
            1. *Efficient in reading small files*
         2. **Faster reads from hot than cold storage**
      4. Both
         1. **Create indexes** - read performance
         2. **Cache - in-memory** - read performance
         3. **paginate the requests**
         4. **Read replicas** - read performance
         5. **Add a load balancer to reduce connections and improve database performance**
         6. **Direct reads to storage/queues** [valet pattern](4_articulatethepattern.md#valet-pattern)
         7. **Separate datastore to split writes and reads when they are both intensive** [CQRS](4_articulatethepattern.md#command-query-responsibility-segregation-cqrs)
   2. [Ways to optimize writes]()
      1. SQL
         1. **Shard**
         2. **Multiple primary**
      2. NoSQL
         1. **Columnar databases**
      3. **Write-back cache to update permanent storage at periodic intervals**
      4. **Add a load balancer to reduce connections and improve database performance**
      5. **Separate datastore to split writes and reads when they are both intensive** [CQRS](4_articulatethepattern.md#command-query-responsibility-segregation-cqrs)
   3. [How to secure data]()
      1. **Encryption and decryption**
   4. [How to save storage cost](7_bottleneck&tradeoffs.md#database-save-disk-cost)
      1. **Differential updates**
      2. **Compression**
         1. [Compression algorithms]()
      3. **Store only references instead of the entire data**
         1. *Use case: Trie in application memory can have less node by merging nodes when there are no branches*
   5. [How does application handle database connection pool]()
   6. [How to handle failed requests to database]()
      1. **Retry those failed requests few times**
   7. [How to log failed requests that have been retried multiple times]()
   8. [How to save development cost](7_bottleneck&tradeoffs.md#in-house-vs-open-source-vs-managed)
      1. **Open source** 
      2. **In-house** - Expensive to develop and maintain
   9. [How to save operational cost](7_bottleneck&tradeoffs.md#in-house-vs-open-source-vs-managed)
      1. **Managed solution** 
      2. **In-house** - Expensive to operate and maintain

### Cache
1. Configurable parameter
   1. [Why do we need cache]()
      1. **Improve read-efficiency by serving content from in-memory datastore**
      2. **Reduce the number of read queries to database**
   2. [What type of content would you cache]()
      1. **Business data**
      2. **static images**
      3. **ML model**
   3. [Where should the cache live?](7_bottleneck&tradeoffs.md#cache-placement)
      1. **Client**
      2. **In edge server** - apigateway
      3. **Local cache - Application memory**
         1. *Advantage: Much faster as connection to external service is avoided*
         2. *Disadvantage: Not a good where cache needs to be invalidated*
      4. **Application disk**
      5. **Remote cache** - redis, memcache
      6. **Database cache**
   4. [How should the cache be updated]()
      1. **Cache aside** - Application calls database to update cache only on cache miss
      2. **Read through** - Cache calls database to update itself. Application calls cache only.
      3. **Write through** - Application updates cache. Cache updates database synchronously.
      4. **Write behind** - Application updates cache. Cache updates database asynchronously.
      5. **Write back** - Update cache only and database at periodic intervals
         1. *Use case: rate-limiting*
         2. *Advantage: Minimal latency added to the user’s requests*
      6. **Refresh ahead** - Change data capture, cache updated once database is updated.
   5. [How much data to cache]()
      1. **All data** - less volume
      2. **20% of the volume** - 80% of the users use 20% of the data
   6. [Who should update the cache]()
      1. **Application writing to database**
      2. **Separate application reading from database** [CDC]()
   7. [When should the cache be updated]()
      1. **Synchronously when the database is updated**
      2. **Asynchronously post database update**
   8. [When should cache be evicted]()
      1. **No eviction policy** - Static data
      2. **Least recently used** - Utilized for fresh data from database
      3. **Least frequently used** - Utilized for hot data
      4. **Polled data from queue** - Utilized for fresh data to be processed
   9. [How long should the cache live]()
      1. **seconds**
      2. **minute** - instant messaging app
      3. **days** - tweets 
      4. **weeks**
      5. **months** - recent news, static data
2. Bottleneck
   1. [How to optimize reads]()
      1. **Create a datastructure to read efficiently**
         1. *Use case: LinkedList ordered based on recency. Clear old data from the end of the list* 
         2. *Use case: Most frequently occuring hashtags*
      2. **Use pagination to cache the next page**
         1. *Use case: paginate based on the client*
      3. **Pre-aggregate based on the read requirement**
         1. *Use case: Aggregate all the tweets from user one follows and merge/sort by time*
   2. [How to optimize storage]()
      1. **Cache the most necessary data**
         1. *Use case: Retweet store the tweet id not the entire content*
   3. [Thundering herd on databases due data not present in cache](7_bottleneck&tradeoffs.md#cache-stampede-or-thundering-herd-or-cache-miss-attack)
      1. **Add null for invalid keys**
      2. **Bloom filter** - to check for valid keys
   4. [Cache node fails]()
      1. **Fallback to secondary cache**
      2. **Make requests to database**
      3. **Re-compute generated data** - better when the computation is not expensive

### Performance

#### Index
Index the data in storage(Application memory, cache, storage)]()
1. Configurable Parameter
   1. [Why do we index data]()
      1. **Speed up read requests**
         1. *Speed up search results*
   2. [Who will index the data]()
      1. **Service which would consume data from message queue and index in search database**
      2. **Map-Reduce setup to periodically index**
   3. [When to index the data]()
      1. **Whenever there is write-request**
         1. *Disadvantage: Resource intensive**
         2. *Disadvantage: Hamper read results**
      2. **Update the index offline at certain interval**
         1. Interval can be based on timestamp or every 1000th write query
         2. *Disadvantage: Serving stale search results*
   4. [What are the different structures to index]()
      1. **Hashtable**
      2. **B-Tree**
      3. **Trie**
      4. **Priority queue**
      5. **Queue**
   5. [Which index to update]()
      1. **Update the existing index**
         1. *Disadvantage: Impact read requests when the update is too long*
      2. **Have a separate index for read and writes**
         1. **Take a copy of the current index, update and overwrite the existing index**
         2. **Queue: Enqeue buffer to hold entries. Once filled, will be dumped to disk; Dequeue buffer will cache entries, Once empty, will read from disk**
      3. **Update the secondary when the primary is taking traffic. Make the secondary as primary and vice versa**
   6. [How to update the index]()
      1. B-Tree and Trie
         1. **Top-down approach**
         2. **Bottom-up approach**
            1. *Use case: Update the trie children with the top result and then update the parent node with the child results**
   7. [Why type of data is indexed]()
      1. **English words nearly 300K**
      2. **Nouns nearly 200K**
2. Bottleneck
   1. [How to speed up indexing]()
      1. **Partition the data**
   2. [How to save storage costs]()
      1. **Do not index words which are not queried**
         1. *Use case: indexing prepositions would exponentially increase the storage cost*

#### Pre-compute
1. Configurable parameters
   1. [What are the ways to pre-compute]()
      1. **Denormalized data to avoid complex joins**
      2. **Responses**
      3. **Materialized views**
2. Advantage
   1. **Queries would be much faster**
3. Disadvantage
   1. **Data redundancy leading to inconsistency**

#### Content Delivery network CDN
1. Configurable parameter
   1. [Why do we need CDN]()
      1. **To reduce latency issues in serving content from a service**
      2. **Better chance of video being closer to user**
      3. **Replicate content in multiple places**
   2. [How many CDNs per region]() - Are the users geographically dispersed
      1. **One CDN per region** - Global CDN
      2. **Primary & multiple secondary CDN per region** - Global + local CDN
      3. **Leaderless multiple CDNs per region** - Local CDNs with peer to peer sync
   3. [How to get data for CDN](7_bottleneck&tradeoffs.md#cdn-overhead-in-updating-the-content)
      1. **Pull content**
      2. **Push content**
         1. *Disadvantage: overhead in updating CDN content*
      3. **Hybrid**
   4. [How does CDN determine whether it can serve content or not]()
      1. **Geographical location of the user**
      2. **Origin of the webpage** - scheme, hostname, port
      3. **Content delivery server has the content**
   5. Bottleneck
      1. [Security checks for CDN](7_bottleneck&tradeoffs.md#cdn-content-authorization-checks)
2. [Caching at the Internet service provider]()
   1. Configurable parameter
      1. [Why do we need caching at the ISP]()
         1.

### Address availability & scaling
1. [Any single point of failure](7_bottleneck&tradeoffs.md#sharding-vs-read-replicas)
   1. [Replicate services/data]() - fallback to be more available
      1. **Read replicas** - improve read performance
         1. *Advantage: Scale read requests easily*
         2. *Disadvantage: Staleness in reading content due to replication lag until the data has been synced from primary*
      2. **Horizontal scaling**
      3. **Content distribution network CDN**
      4. **Backup**
   2. [Partition data]() - minimize failure
      1. **Sharding** - improve write performance
      2. **Vertical partitioning** - improve read and write performance
   3. [How to scale availability]()
      1. [Single region]()
         1. **Multiple availability zone**
         2. **Multiple data center**
      2. [Multiple region]()

#### Sharding
Sharding or Horizontal partitioning - Huge data(>1TB). Write intensive.
1. [Single region]()
   1. Configurable parameter
      1. [Why do we need to shard]()
         1. **Maximize user performance**
         2. **Distribute load on the servers**
         3. **Higher efficiency**
         4. **Lower latencies**
      2. [Which layer to shard]()
         1. **Application**
         2. **Database**
         3. **cache**
      3. [Which layer does the routing](7_bottleneck&tradeoffs.md#sharding-routing-at-application-layer-vs-external-proxy)
         1. **Application layer**
         2. **External proxy**
      4. [Based on what should we split data](7_bottleneck&tradeoffs.md#service-routing---based-on-what-should-we-split-data)
         1. **UserId** - merchants, companies
            1. *Advantage: Easy to query a single shard for user data*
            2. *Disadvantage: Hot/popular users problem - need to make a lot of requests*
            3. *Disadvantage: User have exploding content*
            4. *Disadvantage: Search for content not specific to user performed on multiple servers*
         2. **ResourceId** - photos, message, tweet
            1. *Advantage: No hot users problem*
            2. *Disadvantage: Hot resource problem*
            3. *Disadvantage: Need to query multiple shard to fetch all the user data*
            4. *Disadvantage: Not possible to perform range query based on timestamp*
         3. **ResourceData** - words in tweet
            1. *Advantage: Easy to query for that particular data*
            2. *Disadvantage: hot shards*
            3. *Disadvantage: uneven distribution in shards*
         4. **Event type**
         5. **Timestamp** - Creation time
            1. *Advantage: Fetching the latest data based on timestamp*
            2. *Disadvantage: Traffic load would not be equally distributed*
            3. *Disadvantage: Data to be written to one server and other servers will be idle*
         6. **ResourceId based on timestamp** - Best of resource and timestamp; use sequencer 
            1. *Advantage: No hot users problem*
            2. *Advantage: Fetching the latest data based on timestamp*
            3. *Advantage: No need to create secondary indexes to query based on timestamp. No loss in write latency*
            4. *Disadvantage: Data to be written to one server and other servers will be idle*
      5. [How should we split the data]()
         1. **Range partition** - A-M, N-Z
            1. *Disadvantage: shard wastage for less common characters*
               1. *Combine those into one shard*
            2. *Disadvantage: unbalanced/hot shards*
            3. *Disadvantage: Not easy to optimize the partition for the best range statically*
         2. **Memory capacity based**
            1. *Use case: Fill the server as long as memory is available*
            2. *Disadvantage: hot shards*
         3. **List partition**
         4. **Hash-based partition** - Hash function map to hash modulo function (resourceId % number of servers)
            1. *Advantage: Minimized hot shards as the distribution is random*
         5. **Consistency hashing** - Hash function map to integer(0 to 256)
            1. *Advantage: no unbalanced/hot shards*
            2. *Advantage: Easier to replace a dead server*
      6. [How to find resourceId-shardId mapping information](7_bottleneck&tradeoffs.md#sharding-once-sharded-how-do-you-find-the-shard)
         1. **Simple map of resourceId to shardId in cache/database** - Range/List partitioning
         2. **Identify shardId from resourceId** 
            1. *Use case: ResourceId could have timestamp to identify shardId* - Timestamp based shardId; Range partitioning
            2. *Use case: ResourceId could have integer to identify shardId* - List partitioning
         3. **Hash on the resourceId** - Hash partitioning
      7. [How are storage sharded](7_bottleneck&tradeoffs.md#sharding-logical-vs-physical)
         1. **Physical shards i.e. multiple nodes**
         2. **Logical shards ie. multiple databases in same node**
      8. [How to find the shardId to databaseHost mapping information]()
         1. **Map managed in config/database**
   2. Bottleneck
      1. [Avoid hot shards i.e. lot of requests](7_bottleneck&tradeoffs.md#sharding-how-to-avoid-hot-shards)
         2. [Avoid non-uniform distribution of storage]()
         3. [Cannot store all data of a resource in one shard]()
         4. **Repartition/redistribute the hot shard**
            1. *add another param in sharding strategy* - say time
         5. **Consistent hashing**
         6. **Cache the hot shard data to not overload the database**
      2. [Aggregation data from multiple shards]() - range based sharding
         1. *Disadvantage: Latency issues on combining resource data from multiple shards*
         2. **Separate service to perform aggregation**
   3. [Multiple region]()
      1. [Shard region based on]()
         1. **location** - US and EU users to different regions

#### Vertical partitioning
1. Configurable Parameter
   1. [How to split services]() - e.g., upload file and update metadata
      1. **Managed by same service**
      2. **Managed by same service with upload and download split to scale**- CQRS
      3. **Managed by two separate service**
2. Bottleneck
   1. [Latency issues: How frequently do we join two tables across services]()
      1. **Less**
      2. **More** - Think about vertical partitioning; Caching

#### Primary-Secondary Replication
1. [Single region]()
   1. Parameter
      1. [why do we replicate]()
         1. **load balancing**
         2. **fault tolerance**
      2. [Who would replicate]()
         1. **Single primary**
         2. **Multiple primary** [](6_scaleandresiliency.md#multi-leader-replication)
         3. **Leaderless** - everyone
      3. [How to replicate](7_bottleneck&tradeoffs.md#replicas-synchronous-vs-asynchronous-replication-in-sql-databases)
         1. **Synchronous replication to all replicas**  - Strong durability, increased latency
         2. **Synchronous replication to few replicas** - Less durability, less latency
         3. **Asynchronous replication**
      4. [Which data to replicate]()
         1. **All data**
         2. **Only necessary data**
      5. [* Consistency vs Availability]()
         1. **Number of quorum reads/writes for consistency**
         2. **Number of quorum read/writes for availability**
      6. [primary/replica: Leader selection algorithm](7_bottleneck&tradeoffs.md#leader-selection-algorithm)
      7. [Leaderless/Multiple primary: Consensus algorithm](6_scaleandresiliency.md#consensus)
         1. **paxos**
         2. **raft**
      8. [Leaderless: where would the coordinator node be](7_bottleneck&tradeoffs.md#leaderless-replication-choice-for-coordinator-node)
         1. **Closest to client**
         2. **random**
      9. [Replication encoding scheme](7_bottleneck&tradeoffs.md#availability-replication-encoding-scheme)
         1. **mirroring** - multiple copies of the same data
         2. **reed-solomon encoding**
   3. [Multiple region]()
      1. Parameter
         1. [How to replicate]()
            1. **Backup and restore**
            2. **Active running and passive not running** - Pilot light
            3. **Active running and passive running** - Warm standby
            4. **Active running and active running**
               1. **Write to a main region and read anywhere**  - Read local and write global
               2. **Write to specific region and read anywhere** - Read local and write partitioned
               3. **Write and read anywhere** - Read local and write local


### Address Resiliency
1. [Service mesh](6_scaleandresiliency.md#service-mesh)
2. [Service proxy](6_scaleandresiliency.md#service-proxy)
   1. [Internal Cross cutting concerns](7_bottleneck&tradeoffs.md#service-ambassador-service-vs-service-proxy-for-cross-cutting-concerns)
      1. **Ambassador service**
      2. **Service proxy**
   2. [Where should the service proxy placed]()
      1. **Before application**
      2. **Before database**
      3. **Before cache**
3. Server tradeoff
   1. [Mechanisms to handle server load]()
      1. [Complete Load shedding]() - load shed to avoid malicious users
         1. **Rate-limiting**
      2. [Partial load shedding](6_scaleandresiliency.md#load-shedding)
         1. **Bulkheading**
      3. [Managing load]() - manage load for authentic users
         1. **Queue-based load leveling** [](6_scaleandresiliency.md#load-leveling) - Automatic managing load
         2. **Auto-scaling** - steady requests
         3. **Application/region failover** - Spiky requests
         4. **Capacity planning** - Spiky requests
         5. **Alerting on load increase** - Manual intervention
   2. [Rate-limiting]()
      1. Configurable parameter
         1. [Why do we need rate-limiting]()
            1. **Prevent security attacks made from machines/bots as real users**
               1. *Use case: Prevent Denial of service (DOS) attacks*
               2. *Use case: Prevent brute-force password attempts*
               3. *Use case: Prevent brute-force credit card transactions*
            2. **Prevent misbehaving clients/scripts**
               1. *Use case: Making a lot of analytics requests impacting transactional requests**
               2. *Use case: Developera calling API for the same information again and again*
            3. **Make revenue by charging for requests more than the allowed limit**
            4. **Save on costs**
            5. **Spikiness in traffic**
         2. [Rate-limiting vs Throttling]()
            1. **Rate Limiting is a process that is used to define the rate and speed at which consumers can access APIs.**
            2. **Throttling is the process of controlling the usage of the APIs by customers during a given period.**
               1. *When a throttle limit is crossed, the server returns HTTP status '429 - Too many requests'*
         3. [What are the different entities to rate-limit on]()
            1. **UserId**
               1. *Disadvantage: User needs to be logged in*
               2. *Disadvantage: User account would be locked when a hacker perform denial of service attack by entering wrong credentials*
            2. **DeviceId**
            3. **Client IP**
               1. *Disadvantage: Multiple users share a single public IP like in an internet cafe*
               2. *Disadvantage: Smartphone users that are using the same gateway*
               3. *Disadvantage: Running out of space tracking huge number of IPv6 addresses available to a hacker*
            4. **Business entities**
               1. *Use case: Maximum credit card transactions*
            5. **User and Client IP**
               1. *Advantage: Better than rate-limiting user and client ip individually*
               2. *Disadvantage: More memory and storage*
            6. **Hybrid**
         4. [How long is the rate-limit window]()
            1. **second**
            2. **minute**
            3. **hour**
            4. **day**
         5. [where should throttling be applied]()
            1. **Apigateway/Web-server by calling the rate-limiter service**
            2. **Every service calling rate-limiter service before processing a request**
               1. *Disadvantage: Increase in latency*
            3. **Every service sending request information asynchronously to and throttling based on inputs from rate-limit service**
         6. [Where would we store the rate-limiter information]()
            1. **Database**
         7. [Where would we store the throttling information]()
            1. **Cache**
            2. **Application memory**
               1. *Disadvantage: Node would not be performing global rate-limiting*
         8. [What are different throttling techniques]()
            1. **Hard throttling**
               1. *API requests cannot cross the throttle limit*
            2. **Soft throttling**
               1. *API request to exceed certain percentage say 10% more than the allowed limit*
            3. **Elastic or dynamic throttling**
               1. *API request to exceed when there are free resources available*
         9. [What are the different rate-limit algorithms]()
            1. **Fixed-window algorithm** - 0 to 60 second of a minute
               1. *Token bucket algorithm*
               2. *Disadvantage: Resetting the ‘StartTime’ at the end of every minute, could allow twice the number of requests per minute.*
            2. **Rolling/Sliding-window with sorted timestamp** - request_time to request_time plus 60
               1. *Disadvantage: Take more space compared to fixed-window algorithm*
            3. **Hybrid: Sliding window with timestamp and counter**
               1. *Advantage: Efficient in space*
      2. Bottleneck
         1. [Consistency issues for rate-limiting]()
   3. [Auto-scaling]()
      1. Configurable parameter
         1. [Parameters to auto-scale]()
            1. **instance created based on schedule**
            2. **instance created based on traffic**
            3. **instance created on-demand**
5. Client tradeoff
   1. [Ways to handle request failure](7_bottleneck&tradeoffs.md#resiliency-client-drop-or-retry-failed-requests)
      1. **Retry** - communication errors that can be corrected by attempting them multiple times
      2. **Retry amplification** [](6_scaleandresiliency.md#retry-amplification)
      3. **Fallback to default values** -  helps resolve communication failures locally
      4. **Timeout** - upper bound to latency
      5. **Circuit breaker** - addresses the problem of accidental denial of service attacks due to retries
      6. **Automatic failover**
      7. **Drop**
   2. [Request retry]()
      1. Configurable parameter
         1. [How to avoid retry storm](7_bottleneck&tradeoffs.md#resiliency-client-retry-requests---exponential-backoff-vs-jitter-to-avoid-retry-storm)
            1. **Exponential backoff**
            2. **Jitter**
            3. **Adaptive reconnect timeouts** [](6_scaleandresiliency.md#timeouts)

### Analytics
1. [Data ingestor]() - See messaging components
2. Data processing
   1. Parameters
      1. [why do we process data]()
         1. Rank data based on user activities such as favorites, search, likes and so on.
         2. Weight some data more than the other based on certain conditions.
         3. Similarity predictions
      2. [When to process data]()
         1. **Stream processing - Real time** - Activity logs, Aggregation, Data enrichment, Data classification, Future predictions; Apache Spark/Flink
         2. **Batch processing - Bulk processing** - Historical reports;  HDFS, Hadoop MapReduce
         3. **Hybrid - verification** - verify results are working as expected
      3. [Batch processing: How frequently do we need to batch](7_bottleneck&tradeoffs.md#analytics-batch-processing---what-is-our-batching-strategy)
         1. **Hourly**
         2. **Monthly**
      4. [How do we process data]()
         1. **Run machine learning algorithms**
            1. *Supervised learning*
            2. *Clustering*
            3. *Simple counting*
            4. *personalization*
            5. *trending data*
3. Data storage
   1. Parameters
      1. [How does the data need to stored]()
         1. **Structured data - Data warehouse** 
            1. *Use case: SQL queries run by business analysts*
         2. **Unstructured data - Data lakes** 
            1. *Use case: Machine learning algorithms used by data scientists*
4. Visualization
   1. Parameters
      1. [What kind of queries to support]() - Query engine
      2. [What kind of visualization to support]() - Visualization

### Security
1. [Authentication]()
   1. Configurable parameter
      1. [How to authenticate user]()
         1. **SessionToken**
      2. [How to authenticate client]()
         1. **mTLS**
         2. **Auth token**
      3. [Authentication failure]()
2. [Authorization]()
   1. Configurable parameter
      1. [What are the different way to authorize]()
         1. **View resource**
         2. **Edit resource**
         3. **Delete resource**
      2. [How to authorize users]()
         1. **user has a permission info on resources**
            1. *Advantage: More scalable when the resources are limited*
         2. **resource with allowed list of users**
      3. [How are permissions represented]()
         1. **List**
         2. **permission bitmap**
      4. [Authorization failure]()
         1. **Return 401 error**

### Observability
1. [Metrics]()
   1. **Daily peak**
   2. **Requests per second**
   3. **Latency**

### Deployment
1. [What are the different way to run your application]()
   1. **Virtual machine**
   2. **Kubernetes**
   3. **Cloud functions**



### Bonus when time permits
1. [API design]()
   1. [Communication protocols]()
   2. [HTTP]()
       1. **HTTP methods**
       2. **Pagination**
       3. **Content and Accept language**
2. [Database schema design]()
    1. [SQL]()
        1. **Normalize schema**
    2. [No SQL]()
        1. **Based on query format**
4. [SaaS Integrations]()
    1. [Payments]()
    2. [Observability]()
5. [Metrics]()
