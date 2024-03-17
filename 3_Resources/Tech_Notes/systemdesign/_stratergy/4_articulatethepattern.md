## Decode the pattern

1. [Architecture pattern](#architecture-patterns)
   1. [Client-Server](#client-server)
   2. [Layered](#layered)
   3. [Model View Controller](#model-view-controller)
   4. [Monolith](#monolith)
   5. [Microservice](#microservice)
   6. [Broker](#broker)
   7. [Event Bus](#event-bus)
   8. [Blackboard](#blackboard)
2. [Database pattern](#database-patterns)
   1. [Database per service](#database-per-service)
   2. [SAGA](#saga-pattern)
   3. [Command Query Responsibility Segregation (CQRS)](#command-query-responsibility-segregation-cqrs)
   4. [Index table](#index-table)
   5. [Materialized view](#materialized-view)
   6. [Valet pattern](#valet-pattern)
   7. [Anti-pattern: Shared database](#shared-database-per-service)
3. [Messaging pattern]()
   1. [Domain Event](#domain-event)
   2. [Event sourcing](#event-sourcing)
   3. [Claim check pattern](#claim-check-pattern)
4. [Messaging publishing pattern](#messaging-publishing-pattern)
   1. [Transactional outbox](#transactional-outbox)
   2. [Transactional log tailing](#transactional-log-tailing)
   3. [Polling publisher](#polling-publisher)
5. [Messaging subscribing pattern](#messaging-subscribing-pattern)
   1. [Denormalizer service](#denormalizer-service)
   2. [Gateway service](#gateway-service)
   3. [Sequential Convoy pattern](#sequential-convoy-pattern)
6. [Integration pattern](#integration-patterns)
   1. [Request/response pattern](#requestresponse-pattern)
   2. [Aggregator pattern](#aggregator-pattern)
   3. [Scatter and Gather pattern](#scatter-and-gather-pattern)
   4. [Pipe and Filter pattern](#pipe-filter-pattern)
   5. [Priority queue pattern](#priority-queue-pattern)
   6. [Routing pattern](#routing-pattern)
   7. [Proxy pattern](#proxy-pattern)
   8. [Ambassador pattern](#ambassador-pattern)
   9. [Branch pattern](#branch-pattern)
   10. [Adapter pattern](#adapter-pattern)
   11. [Sort data pattern](#sort-data-pattern)
   12. [Sequence data pattern](#sequence-data-pattern)
   13. [Anti-pattern: Chained pattern](#chained-pattern)
7. [Communication pattern](#external-communication-patterns)
   1. [API gateway pattern](#api-gateway-composition)
   2. [Backend for frontend pattern](#backend-for-frontend-pattern)
   3. [Anti-corruption layer](#anti-corruption-layer)
8. [Decomposition Pattern - Green field project](#decomposition-patterns---green-field-projects)
   1. [Decompose by Business functionality](#decompose-by-business-functionality)
   2. [Decompose by subdomain](#decompose-by-subdomain)
   3. [Decompose by transactions](#decompose-by-transactions)
9. [Decomposition Pattern - Brown field project](#decomposition-patterns---brown-field-projects)
   2. [Strangler pattern](#strangler-pattern)
   3. [Anti-corruption layer](#anti-corruption-layer)
   4. [Bulkhead pattern]()
10. [Deployment Pattern](#deployment-patterns)
    1. [Multiple service instances per host]()
    2. [Service instances per host]()
    3. [Service instance per VM]()
    4. [Service instance per container]()
    5. [Serverless deployment]()
    6. [Service deployment platform]()
    7. [Sidecar pattern]()

### Architecture patterns

#### Client-server 
* Typical real world use cases of this pattern include online applications such as email, document sharing and banking. 
* Server provides the service and the client consumes it. 
* Usually server has a huge computing power but bound to a limit. There are chances that the server may crash or stop responding when the traffic overwhelming. 
* This happens to web apps hosted with cloud and on-premises as well.

#### Layered 
* It is also known as N-Tier architecture. 
* In here, software is divided into units called layers.
* This usually contains 4 different as follows:
  * Presentation Layer
  * Application Layer
  * Business Logic Layer
  * Data Access Layer
* Usually, this pattern used in desktop and simple web applications.

#### Model-view-controller
* It separates the application functionality into three kinds of components 
  * Model which contains the core functionality and data 
  * View which displays the information to user where more than one view may be defined 
  * Controller which handles the input from the user 
* Commonly used in web frameworks such as ASP.NET, Django.

#### Monolith

#### Microservice

#### Broker

#### Blackboard
* This pattern is useful for problems for which no deterministic solution strategies are known. 
* The Blackboard pattern consists of three main components:
  * Blackboard which is a structured global memory containing objects from the solution space.
  * Knowledge Source which is specialized module with their own representation.
  * Control Component which selects configures and executes modules.
* All the components have access to the blackboard.
* Components may produce new data objects that are added to the blackboard.
* Components look for particular kinds of data on the blackboard and may find these by pattern matching with the existing knowledge source.
* The advantage of using this pattern is the extending the structure of the data space is easy however modifying the structure of the data space is hard as all applications are affected.
* This pattern is often used in speech recognition, protein structure identification and robotics.

### Database patterns

#### Database per service

#### Command Query Responsibility Segregation (CQRS)
* Split the reads and writes
  * Commands are consumed by Model Services to update the model
  * Events are produced that are consumed by Denormalizer or Gateway Services which update Read models
  * Queries are then made against the Read model
* Solution here might be CQRS that separates those reads and writes into different components commands for updating, queries for reading:
  * Commands have to be task-based (“Book hotel room”, not “set ReservationStatus to Reserved”). 
  * Commands implemented through asynchronous communication 
  * Queries never alter the database. A query responses with a DTO that does not hold business logic. 
* One Drawback in this pattern is holding read and write components synchronized.
* When to use:
  * Collaborative domains where many users access the same data in parallel. 
    * CQRS allows you to define commands with enough granularity to minimize merge conflicts at the domain level, and conflicts that do arise can be merged by the command.
  * Task-based user interfaces where users are guided through a complex process as a series of steps or with complex domain models. 
    * The write model has a full command-processing stack with business logic, input validation, and business validation. 
    * The write model may treat a set of associated objects as a single unit for data changes (an aggregate, in DDD terminology) and ensure that these objects are always in a consistent state. 
    * The read model has no business logic or validation stack, and just returns a DTO for use in a view model. 
    * Scenarios where performance of data reads must be fine-tuned separately from performance of data writes, especially when the number of reads is much greater than the number of writes. 
      * In this scenario, you can scale out the read model, but run the write model on just a few instances. 
      * A small number of write model instances also helps to minimize the occurrence of merge conflicts.
    * The read model is eventually consistent with the write model.
    * Scenarios where the system is expected to evolve over time and might contain multiple versions of the model, or where business rules change regularly.
    * Integration with other systems, especially in combination with event sourcing, where the temporal failure of one subsystem shouldn't affect the availability of the others.
  * Scenarios where one team of developers can focus on the complex domain model that is part of the write model, and another team can focus on the read model and the user interfaces.
* When to not use: 
  * domain or the business rules are simple.
  * simple CRUD-style user interface and data access operations are sufficient.

#### Index table

#### Materialized view
* When to use this pattern
  * Creating materialized views over data that's difficult to query directly, or where queries must be very complex to extract data that's stored in a normalized, semi-structured, or unstructured way. 
  * Creating temporary views that can dramatically improve query performance, or can act directly as source views or data transfer objects for the UI, for reporting, or for display. 
  * Supporting occasionally connected or disconnected scenarios where connection to the data store isn't always available. 
    * The view can be cached locally in this case. 
  * Simplifying queries and exposing data for experimentation in a way that doesn't require knowledge of the source data format. For example, by joining different tables in one or more databases, or one or more domains in NoSQL stores, and then formatting the data to fit its eventual use. 
  * Providing access to specific subsets of the source data that, for security or privacy reasons, shouldn't be generally accessible, open to modification, or fully exposed to users. 
  * Bridging different data stores, to take advantage of their individual capabilities. For example, using a cloud store that's efficient for writing as the reference data store, and a relational database that offers good query and read performance to hold the materialized views. 
  * When using microservices, you are recommended to keep them loosely coupled, including their data storage. Therefore, materialized views can help you consolidate data from your services. If materialized views are not appropriate in your microservices architecture or specific scenario, please consider having well-defined boundaries that align to domain driven design (DDD) and aggregate their data when requested.
* When to not use this pattern
  * The source data is simple and easy to query. 
  * The source data changes very quickly, or can be accessed without using a view. 
    * In these cases, you should avoid the processing overhead of creating views. 
  * Consistency is a high priority. The views might not always be fully consistent with the original data.

#### Valet pattern
* Use a token that provides clients with restricted direct access to a specific resource, in order to offload data transfer from the application. 
* This is particularly useful in applications that use cloud-hosted storage systems or queues, and can minimize cost and maximize scalability and performance.
* When to use
  * To minimize resource loading and maximize performance and scalability. 
    * Using a valet key doesn't require the resource to be locked, no remote server call is required, there's no limit on the number of valet keys that can be issued, and it avoids a single point of failure resulting from performing the data transfer through the application code. 
    * Creating a valet key is typically a simple cryptographic operation of signing a string with a key.
  * To minimize operational cost. 
    * Enabling direct access to stores and queues is resource and cost efficient, can result in fewer network round trips, and might allow for a reduction in the number of compute resources required.
  * When clients regularly upload or download data, particularly where there's a large volume or when each operation involves large files.
  * When the application has limited compute resources available, either due to hosting limitations or cost considerations. 
    * In this scenario, the pattern is even more helpful if there are many concurrent data uploads or downloads because it relieves the application from handling the data transfer.
  * When the data is stored in a remote data store or a different datacenter. If the application was required to act as a gatekeeper, there might be a charge for the additional bandwidth of transferring the data between datacenters, or across public or private networks between the client and the application, and then between the application and the data store.
* When to not use
  * If the application must perform some task on the data before it's stored or before it's sent to the client. 
    * For example, if the application needs to perform validation, log access success, or execute a transformation on the data. 
    * However, some data stores and clients are able to negotiate and carry out simple transformations such as compression and decompression (for example, a web browser can usually handle gzip formats).
  * If the design of an existing application makes it difficult to incorporate the pattern. 
    * Using this pattern typically requires a different architectural approach for delivering and receiving data.
  * If it's necessary to maintain audit trails or control the number of times a data transfer operation is executed, and the valet key mechanism in use doesn't support notifications that the server can use to manage these operations.
  * If it's necessary to limit the size of the data, especially during upload operations. 
    * The only solution to this is for the application to check the data size after the operation is complete, or check the size of uploads after a specified period or on a scheduled basis.

#### SAGA Pattern
Ref. Tradeoffs to learn more about SAGA pattern

#### Shared database per service
* Anti-pattern for microservices

#### Event Sourcing
* Ability to rebuild the full state of the system by a persisted log of events
* Event Sourcing works with your data like version control systems work with your code
* Event notification
    * Asynchronous + Push data
    * Generic code notifies specific code by events
    * Pro: Decoupling
    * Con's: inability to understand what is going on by stepping through the code
* Event-carried State Transfer
    * Asynchronous + Push data
    * Subscribers don't ask for additional information after an event occured, all necessary state is given in the events.
    * Subscribers copy whatever they need.
    * Pro's: can greatly reduce network traffic. Better availability because of the copied data
    * Con's: consistency
* When to use
  * When you want to capture intent, purpose, or reason in the data. 
    * For example, changes to a customer entity can be captured as a series of specific event types, such as Moved home, Closed account, or Deceased.
  * When it's vital to minimize or completely avoid the occurrence of conflicting updates to data.
  * When you want to record events that occur, and be able to replay them to restore the state of a system, roll back changes, or keep a history and audit log. 
    * For example, when a task involves multiple steps you might need to execute actions to revert updates and then replay some steps to bring the data back into a consistent state.
  * When using events is a natural feature of the operation of the application, and requires little additional development or implementation effort.
  * When you need to decouple the process of inputting or updating data from the tasks required to apply these actions. 
    * This might be to improve UI performance, or to distribute events to other listeners that take action when the events occur. 
    * For example, integrating a payroll system with an expense submission website so that events raised by the event store in response to data updates made in the website are consumed by both the website and the payroll system.
  * When you want flexibility to be able to change the format of materialized models and entity data if requirements change, or—when used in conjunction with CQRS—you need to adapt a read model or the views that expose the data.
  * When used in conjunction with CQRS, and eventual consistency is acceptable while a read model is updated, or the performance impact of rehydrating entities and data from an event stream is acceptable.
* When to not use
  * Small or simple domains, systems that have little or no business logic, or nondomain systems that naturally work well with traditional CRUD data management mechanisms.
  * Systems where consistency and real-time updates to the views of the data are required.
  * Systems where audit trails, history, and capabilities to roll back and replay actions are not required.
  * Systems where there's only a very low occurrence of conflicting updates to the underlying data. 
    * For example, systems that predominantly add data rather than updating it.

### Claim check pattern

#### Write ahead logging

#### Domain Event

### Messaging publishing pattern

#### Transactional Outbox

#### Transactional log tailing
* Change data capture (CDC)
  * Bin logs used for master-slave replication
  * Asynchronous + Push data

#### Polling publisher

### Messaging subscribing pattern

#### Denormalizer service
* Denormalizers are exactly what Relational databases are doing, except, for a distributed system. 
* They are joining together multiple normalized sources of input into a readable data structure that a client can consume.
* For example, imagine you have an e-commerce app. When stock levels increase or decrease, or, become available in your inventory, your application should know about it.
* This means with a denormalizer service you are subscribing to the events being emitted from the Model service above, and if you are using MongoDb, using something like mongoose to persist that data in a perfect structure for that particular application to consume.

#### Gateway service
* Gateway Services can be used very similarly to Denormalizers. Instead of connecting to a database, however, it is a connection to an API.
* Recommendation engine, called LiftIgniter, needed to be synchronized with an inventory. 
* The service subscribes to inventory.product.updated and inventory.product.added events, and simply POSTs the formatted data to the appropriate endpoints.

#### Sequential Convoy pattern
* Process a set of related messages in a defined order, without blocking processing of other groups of messages.
* Applications often need to process a sequence of messages in the order they arrive, while still being able to scale out to handle increased load.
* Use this pattern when:
  * You have messages that arrive in order and must be processed in the same order. 
  * Arriving messages are or can be "categorized" in such a way that the category becomes a unit of scale for the system. 
* This pattern might not be suitable for:
  * Extremely high throughput scenarios (millions of messages/minute or second), as the FIFO requirement limits the scaling that can be done by the system.
* Source: https://docs.microsoft.com/en-us/azure/architecture/patterns/sequential-convoy

### Integration patterns

#### Request/response pattern
* Synchronously make a call from one service to another
* Asynchronously make a request via a queue
  * In this pattern a sender posts a message to a queue and expects a response from the receiver. 
  * You can use this pattern to implement a reliable system where you must confirm that a message has been received and processed. 
  * If the response is not delivered within a reasonable interval, the sender can either send the message again or handle the situation as a timeout or failure. 
  * This pattern usually requires a separate communications channel in the form of a dedicated message queue to which the receiver can post its response messages 
    * (the sender can provide the details of this queue as part of the message that it posts to the receiver). 
  * The sender listens for a response on this queue. 
  * This pattern typically requires some form of correlation to enable the sender to determine which response message corresponds to which request sent to the receiver.
  
#### Aggregator pattern
* When breaking the business functionality into several smaller logical pieces of code, it becomes necessary to think about how to collaborate the data returned by each service.
* Use cases:
  * Reuse computation
  * In-memory computation - reconciling, sorting
  * Prioritized computation - Weighted graph

#### Routing pattern
* Routing requests to the corresponding service.
* 


#### Proxy pattern
* Proxy may be a dumb proxy in which case it just delegates the request to one of the services. 
* Alternatively, it may be a smart proxy where some data transformation is applied before the response is served to the client. 
* A good example of this would be where the presentation layer to different devices can be encapsulated in the smart proxy.

#### Ambassador pattern
* Ambassador pattern is often used to extend network abilities of existing service, especially for the cases that this service is old or complex enough to modify.
* Create helper services that send network requests on behalf of a consumer service or application. 
* An ambassador service can be thought of as an out-of-process proxy that is co-located with the client.
* Pattern can be useful for offloading common client connectivity tasks such as monitoring, logging, routing, security (such as TLS), and resiliency patterns in a language agnostic way.
* When to use
  * Need to build a common set of client connectivity features for multiple languages or frameworks. 
  * Need to offload cross-cutting client connectivity concerns to infrastructure developers or other more specialized teams. 
  * Need to support cloud or cluster connectivity requirements in a legacy application or an application that is difficult to modify.
* when to not use
  * When network request latency is critical. A proxy will introduce some overhead, although minimal, and in some cases this may affect the application. 
  * When client connectivity features are consumed by a single language. In that case, a better option might be a client library that is distributed to the development teams as a package. 
  * When connectivity features cannot be generalized and require deeper integration with the client application.


#### Branch pattern
* Service A, either a web page or a composite microservice, can invoke two different chains concurrently in which case this will resemble the Aggregator design pattern. 
* Alternatively, Service A can invoke only one chain based upon the request received from the client.

#### Scatter and Gather pattern
* Use case:
  * Divide and conquer computation - finding the nearest cab in the closest map segment

#### Pipe-filter pattern
* Pipe and Filter is an architectural pattern for stream processing. 
* It consists of one or more components called filters. 
* These filters will transform or filter data and then pass it on via connectors called pipes
* Decompose a task that performs complex processing into a series of separate elements that can be reused.
* Use this pattern when:
  * The processing required by an application can easily be broken down into a set of independent steps. 
  * The processing steps performed by an application have different scalability requirements. 
  * It's possible to group filters that should scale together in the same process. For more information, see the Compute Resource Consolidation pattern. 
  * Flexibility is required to allow reordering of the processing steps performed by an application, or the capability to add and remove steps. 
  * The system can benefit from distributing the processing for steps across different servers. 
  * A reliable solution is required that minimizes the effects of failure in a step while data is being processed. 
* This pattern might not be useful when:
  * The processing steps performed by an application aren't independent, or they have to be performed together as part of the same transaction. 
  * The amount of context or state information required by a step makes this approach inefficient. It might be possible to persist state information to a database instead, but don't use this strategy if the additional load on the database causes excessive contention.

#### Priority queue pattern

#### Adapter pattern
* Convert from one format to another
* Also called Anti-corruption layer
* Use this pattern when:
  * A migration is planned to happen over multiple stages, but integration between new and legacy systems needs to be maintained. 
  * Two or more subsystems have different semantics, but still need to communicate. 
* This pattern may not be suitable if there are no significant semantic differences between new and legacy systems.

#### Dedupe pattern
* Dedupe or accept duplicates
* Data deduplication is a technique used for eliminating duplicate copies of data to improve storage utilization.
* It can also be applied to network data transfers to reduce the number of bytes that must be sent. 
* For each new incoming content, we can calculate a hash of it and compare that hash with all the hashes of the existing content to see if we already have the same content present in our storage.
* Post-process deduplication 
  * With post-process deduplication, new content are first stored on the storage device and later some process analyzes the data looking for duplication. 
  * The benefit is that clients will not need to wait for the hash calculation or lookup to complete before storing the data, thereby ensuring that there is no degradation in storage performance. 
  * Drawbacks of this approach are 
    1) We will unnecessarily be storing duplicate data, though for a short time, 
    2) Duplicate data will be transferred consuming bandwidth.
* In-line deduplication 
  * Alternatively, deduplication hash calculations can be done in real-time as the clients are entering data on their device. 
  * If our system identifies a content that it has already stored, only a reference to the existing content will be added in the metadata, rather than a full copy of the chunk. 
  * This approach will give us optimal network and storage usage.

#### Verifier/Reconciliation pattern

#### Sort data pattern
* Order data based on the single or multiple field.
* Multiple fields can also be smartly combined into a single field say epoch timestamp + auto-generated sequence id
  * Auto-generated sequence id can be started from 1 every second.

#### Sequence data pattern
* Single database/Cache
  * Easier to generate a sequence number
  * Single point of failure
* Two database/cache
  * One generates odd number
  * other generates even number
  * When one server goes down, other server can be responsible for generatign sequence
* Best solution: Epoch timestamp + machine id + sequence no

#### Search data pattern

#### Cleaning historical or expired data

#### Compute Resource Consolidation pattern
* Consolidate multiple tasks or operations into a single computational unit.
* Applies to App Services, Container Apps, and Virtual Machines.
* Tasks can be grouped according to criteria based on the features provided by the environment and the costs associated with these features.
* When to use this pattern?
  * Use this pattern for tasks that are not cost effective if they run in their own computational units. 
    * If a task spends much of its time idle, running this task in a dedicated unit can be expensive.
  * pattern might not be suitable for tasks that perform critical fault-tolerant operations, or tasks that process highly sensitive or private data and require their own security context. 
    * These tasks should run in their own isolated environment, in a separate computational unit.

#### Chained pattern

### External communication patterns

#### API Gateway composition

#### Backend for frontend pattern
* Create separate backend services to be consumed by specific frontend applications or interfaces.
* Use this pattern
  * A shared or general purpose backend service must be maintained with significant development overhead.
  * You want to optimize the backend for the requirements of specific client interfaces.
  * Customizations are made to a general-purpose backend to accommodate multiple interfaces.
  * An alternative language is better suited for the backend of a different user interface.
* You don't use this pattern
  * When interfaces make the same or similar requests to the backend.
  * When only one interface is used to interact with the backend.

#### Anti-corruption layer

### Decomposition patterns - Green field projects

####  Decompose by business functionality
* Define services corresponding to business capabilities.
* business capability often corresponds to a business object, e.g.
    * Order Management is responsible for orders
    * Customer Management is responsible for customers

#### Decompose by subdomain
* Decomposing an application using business capabilities might be a good start,
    * you will come across so-called “God Classes” which will not be easy to decompose
* Define services corresponding to Domain-Driven Design (DDD) subdomains.
* DDD refers to the application’s problem space — the business — as the domain.
* Subdomains can be classified as follows:
    * Core — key differentiator for the business and the most valuable part of the application
    * Supporting — related to what the business does but not a differentiator.
        * These can be implemented in-house or outsourced
    * Generic — not specific to the business and are ideally implemented using off the shelf software
* Subdomains of an Order management include:
    * Product catalog service
    * Inventory management services
    * Order management services
    * Delivery management services

#### Decompose by transactions
* Decompose services over the transactions.
* Ideal strategy is to use 2 phase commit. Though does not work well on high-scale.

### Decomposition patterns - Brown field projects

#### Strangler pattern
* Newly refactored application strangles or replaces the legacy one
  * Creates two separate applications that live side by side in the same URI space. 
  * Over time, the newly refactored application “strangles” or replaces the original application until finally, you can shut off the monolithic application.
* Steps
  * Transform — Create a parallel new site with modern approaches. 
  * Coexist — Leave the existing site where it is for a time. 
    * Redirect from the existing site to the new one so the functionality is implemented incrementally. 
  * Eliminate — Remove the old functionality from the existing site.

#### BulkHead pattern
See scalability section.

### Deployment patterns
* Separate service (On a separate node)
* Library (Part of the service process)

#### Sidecars
* Examples
  * Infrastructure API. The infrastructure development team creates a service that's deployed alongside each application, instead of a language-specific client library to access the infrastructure. The service is loaded as a sidecar and provides a common layer for infrastructure services, including logging, environment data, configuration store, discovery, health checks, and watchdog services. The sidecar also monitors the parent application's host environment and process (or container) and logs the information to a centralized service. 
  * Manage NGINX/HAProxy. Deploy NGINX with a sidecar service that monitors environment state, then updates the NGINX configuration file and recycles the process when a change in state is needed.
  * Ambassador sidecar. Deploy an ambassador service as a sidecar. The application calls through the ambassador, which handles request logging, routing, circuit breaking, and other connectivity related features. 
  * Offload proxy. Place an NGINX proxy in front of a node.js service instance, to handle serving static file content for the service.

### Resources
* https://medium.com/interviewnoodle/10-software-architecture-patterns-in-enterprise-software-development-fabacb5ed0c8
* https://www.abhishek-tiwari.com/object-inspired-container-design-patterns/
* https://medium.com/@madhukaudantha/microservice-architecture-and-design-patterns-for-microservices-e0e5013fd58a
* https://docs.microsoft.com/en-us/azure/architecture/patterns/