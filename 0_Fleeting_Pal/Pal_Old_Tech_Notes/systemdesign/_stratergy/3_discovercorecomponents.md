# List the architecture components
Listing the architectural components is all about cloud architecture diagrams.
That is, what cloud services do you need to enable your service?
Do you need a server like Amazon’s EC2? Or simple file storage like Amazon’s S3?
If you’re not comfortable drawing cloud architecture diagrams, do take a moment to practice.

Note: this session should focus on communication and coordination.
Later on, we can focus on scalability, resiliency and reliability later on. 

## Components
Processing and Computation
1. [Frontend - Web tier](#frontend---web-tier)
2. [Backend - stateless](#backend---stateless)
3. [Backend - stateful](#backend---stateful)
4. [Serverless](#serverless)
Scheduler
5. [Schedule job](#schedule-jobs)
6. [Workflow task orchestration](#workflow-tasks-orchestration)
Storage - Structured
7. [SQL - OLTP](#storage---sql---oltp---rdms)
Storage - Semi Structured
8. [Keyvalue store](#storage---nosql---keyvalue-store)
9. [Keyvalue store - in-memory](#storage---nosql---keyvalue-store---in-memory)
10. [NoSQL - Document datastore](#storage---nosql---document-data-store)
11. [NoSQL - Wide column datastore](#storage---nosql---wide-column-datastore)
12. [NoSQL - Graph database](#storage---nosql---graph-databases)
13. [Search Data](#storage---text-search)
14. [Geospatial](#storage---geospatial)
15. [Immutable Ledger](#storage--immutable-ledger)
16. [Time series database](#storage---time-series-database)
Storage - Unstructured
17. [File storage](#storage---files)
18. [Block storage](#storage---block)
19. [Object storage](#storage---object)
Storage - Big data
20. [Storage - Data warehouse - OLAP](#storage---data-warehouse)
21. [Storage - Data lake](#storage---data-lake)
Messaging
22. [Storage - Streaming SQL](#storage---streaming-sql)
23. [Data ingestion - Message Queue](#data-ingestion---message-queue)
24. [Data ingestion - Notification Service](#data-ingestion---notification-service)
25. [Data ingestion - Publisher subscriber](#data-ingestion---publisher-subscriber)
26. [Data ingestion - Change data capture](#data-ingestion---change-data-capture)
Data infrastructure
27. [Data processing - Batch](#data-processing---batch)
28. [Data processing - Stream](#data-processing---stream)
29. [Data integration - ETL/ELT](#data-integration---etlelt)
30. [Analytics - Query Engine](#analytics---query-engine)
31. [Analytics - Business Intelligence](#analytics---visualization---business-intelligence)
32. [Analytics - Operational Intelligence](#analytics---visualization---operational-intelligence)

### Frontend - Web tier
* Where web pages are served, 
  * usually combined with the service / backend tier in the very early stage of a web service.
* MVC(MVT) or MVVC pattern is the dominant pattern for this layer. 
  * Traditionally, view or template is rendered to HTML by the server at runtime. 
  * In the age of mobile computing, view can be as simple as serving the minimal package of data transporting to the mobile devices, which is called web API. 
  * People believe that the API can be shared by clients and browsers. 
  * And that is why single page web applications are becoming more and more popular, 
    * especially with the assistance of frontend frameworks like react.js, angular.js, backbone.js, etc.

### Backend - Stateless
* Threads, Task Executors
* perform few operations in-memory (or with the help of cache) before sending to storage
  * dedupe, aggregate results
* Single responsibility principle advocates small and autonomous services that work together, 
  * so that each service can do one thing well and not block others.
* push or pull data

### Backend - Stateful
* Use cases - Gaming

### Schedule jobs
* Schedule batch jobs
* Software:
  * Opensource: Java Quartz
  * Commercial:
  * AWS: 
  * Azure: 
  * GCP: kubernetes cronjob

### workflow tasks orchestration
* Much better than job scheduler as you can 
  * Manage dependencies on tasks
  * Re-run only the failed tasks instead of the entire job.
* Software:
  * Opensource: Apache airflow
  * Commercial:
  * AWS:
  * Azure:
  * GCP: Cloud composer (Managed airflow)

### Serverless
* Run small computations based on a request
* Software
  * Cloud Agnostic: 
  * GCP: Cloud-run

### Storage - SQL - OLTP - RDMS
* Purpose: Capture, store, and process data from transactions in real-time
  * Ideal for data with relationships 
  * OLTP applications need datastores that support low latency reads and writes of individual records.
  * Tables are normalized for reduced data redundancy and better data integrity.
* Physical level: B+ index tree for sorting and filtering
* Conceptual level: rows and columns (relations between entities)
* External level: simple CRUD, complicated aggregation, nested queried data
* Transactional guarantees - ACID
* CAP (Consistency, Availability and Partition tolerance)
  * Single node: CA
  * Master: Read and writes to master, then it CP
  * Master-slave: Reads to replica and writes to master, it is AP when replicas go down or CP when master goes down.
  * Master-Master: Read and writes to multiple masters, then it is AP
* Replication
  * Master-slave
  * Master-Master
* Poor performance reasons
  * Querying one row at a time for aggregation
  * No index on filter conditions, order by, aggregated queries
* Data-limits
  * SQL Server allows a maximum of 32767 concurrent connections
  * MySQL databases handle over 25,000 SQL queries per second.
  * Database can have 1TB of storage.
  * More than these limitations, you need to shard the data. 
* Software: 
  * Cloud agnostic: MySQL, PostGreSQL, SQL server, Oracle, DB2, KSQLDB
  * AWS: Amazon Aurora, Relational database service(RDS)
  * Azure: Azure SQL database
  * GCP: Cloud SQL (Managed MySQL, Hive - No horizontal scalability), Cloud spanner (Managed, horizontal scalability)
* Use case: OLTP, customer metadata, payment, orders

###  Storage - NoSQL - Key/Value Store - In-memory
* Purpose: Faster cache lookup based in-memory
  * It eliminates the disk IO overhead and serves as a fast cache.
  * Optimized for faster reads
* Persistence
  * Redis supports data persistence
  * Memcache does not
* Data-limits
  * Redis server can process 80,000 to 100,000 QPS
  * Redis can handle 10,000 client connections available.
  * Maximum size that can be stored: 144GB
* Software
  * Open Source: Redis, Memcached, Etcd(Kubernetes), Voldermont, Riak
  * Cloud Agnostic: Hazelcast, Ignite
  * AWS: Elasticcache
  * Azure: Azure cache for redis
  * GCP: Memory-store
* Use cases - Session-storage, Cache responses, Time to live temporary data, Plenty of read requests

###  Storage - NoSQL - Key/Value Store
* Purpose: Faster lookup based on key-value store is a dictionary or hash table database
  * Optimized for faster reads
* Physical level: 
* Conceptual level: hashmap (key-value pairs)
* External level: 
* Aggregate data store where the value can be used to store any aggregate (group of data)
* CAP (Consistency, Availability and Partition tolerance)
  * Dynamo DB - AP
  * Redis - CP
* Software
  * Cloud Agnostic: Redis, Scylia DB, Ignite
  * AWS: DynamoDB
  * Azure: Cosmos DB
  * GCP: Bigtable (Managed), Memory-store (Managed redis/memcache)
* Use cases - Rate-limiting, Persisted and in-memory data

### Storage - NoSQL - Document data store
* Purpose: Document stores are for storing and retrieving a document consisting of nested objects. a tree structure such as XML, JSON, and YAML.
* Physical Level:
* Conceptual level: KV Pair where values are XML, JSON, BSONs document
* External level: Simple CRUD, complicated aggregation, nested queried data
* Transactional integrity: BASE
* Aggregate data store where the document can be used to store any aggregate (group of data)
* Aggregate updates are going to be atomic.
  * Problem is when you update multiple aggregates which is not atomic.
* Even though it is schemaless, we mostly deal with implicit assumptions on the schema.
* CAP (Consistency, Availability and Partition tolerance)
  * Mongo DB - CP
* Replication
  * Master: Read and writes to master, then MongoDB is CP (Default behavior)
  * Master-slave: Reads to replica and writes to master, it is AP for read requests (Read preference mode in MongoDB)
  * Master-slave: Set majority nodes for a write to be replicated, it is CP (Write preference mode in MongoDB)
* Poor performance
  * Data is very huge to store in JSON format
* Software
  * Open Source: MongoDB, Couchbase, Expresso (LinkedIn)
  * Cloud Agnostic: Solr, Terrastore, OrientDB, RavenDB
  * AWS: Document DB
  * Azure: Cosmos DB
  * GCP: Firestore
* Use case: Item Catalog, Item aggregation

### Storage - NoSQL - Wide-Column datastore
* Purpose: 
  * highly-available, geographical distribution
  * data indexed based on timestamps 
  * finite read queries
  * data is optimized for writes/inserts
  * decent enough for updates
  * data is rarely deleted
* Insufficient query pattern
  * Fetching data from multiple partitions – this will require a coordinator to fetch the data from multiple nodes, store it temporarily in heap, and then aggregate the data before returning results to the user
  * Bad at support for joins, group by, OR clause, aggregations, etc.
* Conceptual level: 
  * Giant nested map (2D key-value )
    * ColumnFamily<RowKey, Columns<Name, Value, Timestamp>>
* External level: infinite queries based on keys (not on anything else)
  * Constraint: partition keys on which all queries should happen.
* CAP (Consistency, Availability and Partition tolerance)
  * HBase - CP
* Replication
  * Asynchronous masterless replication: AP for Cassandra (Default configuration)
  * Quorum consistency level set to ANY/ONE: AP for Cassandra
  * Quorum consistency level set to QUORUM/ALL: CP for Cassandra
  * master-based replication (HBase)
* Data limits
  * Cassandra can perform 1 million writes per second.
* Software
  * Cloud Agnostic: HBase, Cassandra, ScyllaDB, Hypertable, 
  * Cloud-Agnostic(Real-time): Druid, Pinot, Clickhouse, Rockset
  * AWS: Keyspaces, Amazon SimpleDB
  * Azure: Cosmos DB
  * GCP: Bigtable (Managed)
* Use cases - Tracking status, History data, Feed data

### Storage - NoSQL - Graph databases
* Purpose
  * store entities and the relationships between them.
  * adding/removing relationships does not involve schema changes and data movement
* Physical level:
* Conceptual level:
* External level:
* Graph databases have ACID properties.
* Software
  * Cloud Agnostic: OrientDB, Neo4j, Giraph
  * AWS: Neptune
  * Azure: Cosmos DB
  * GCP: JanusGraph + BigTable (Managed)

### Storage - text search
* Text search on unstructured (natural) or semi-structured text is a common operation in many applications
  * text + fuzzy search
  * Unbounded data size
  * text can either be plain or rich (e.g. PDF), stored in 
    * a document database
    * a blob store
* Adhoc query pattern
* Can have multiple tags i.e. size, cost and so on to identify items
* Software
  * Cloud Agnostic: Elastic search, Solr, Elassandra
  * AWS: Elastic search, Cloud search
  * Azure: Cognitive search
  * GCP: Search APIs on the datastores

### Storage - Geospatial
* Purpose
  * Geospatial database is a database to store geographic data (such as countries, cities, etc.). 
  * It is optimized for geospatial queries and geometric operations.
  * Wide column, key-value, document, or relational database with geospatial queries is commonly
  * Analytics use cases, a columnar database may suit better.
* Software
  * Cloud Agnostic: Solr, PostGIS, MongoDB (GeoJSON)
  * AWS: Keyspaces
  * Azure: Cosmos DB
  * GCP: Bigtable (Managed), Bigquery

### Storage - Time series database
* Purpose
  * time series is a series of data points, indexed and ordered by timestamp. 
  * The timestamp is the key in the Time Series datastores.
  * A time series can be modeled as:
    * **Key-value:** associated pairs of timestamps and values
    * **Wide column:** with the timestamp as the key for the table 
      * A wide column store with date-time functions from the programming languages is often used as a time series database.
    * In analytics use cases, a columnar database can be used for time-series data as well.
* Append only-write mode. No overwrites.
* Software
  * Cloud Agnostic: OpenTSDB, InfluxDB, ScyliaDB
  * AWS: Timestream
  * Azure: Cosmos DB
  * GCP: Bigtable (Managed), BigQuery
* Use case: system metrics

### Storage- Immutable ledger
* Purpose:
  * Immutable Ledger is for maintaining an immutable and (cryptographically) verifiable transaction log owned by a central trusted authority.
  * From the storage perspective, a wide column store suffices. 
  * But datastore operations must be immutable and verifiable.
* Software
  * Cloud Agnostic: Hyperledger Fabric
  * AWS: Quantum Ledger Database (QLDB)
  * Azure: Azure SQL Database Ledger
  * GCP:

### Storage - Files
* Binary Large OBjects(Blob) storage is the hyper-scale distributed version of the filesystem
  * Blob supports CRUD (create, read, update, delete) operations at the file level.
  * The directory or file path is the index.
  * you can quickly locate and read the file. 
  * locating something within a file requires a sequential scan
* Data is stored as files under a hierarchical directory structure.
* Most common general-purpose storage solution.
* Made accessible by a large number of servers using common file-level network protocols like SMB/CIFS and NFS.
* Servers accessing file storage do not need to deal with the complexity of managing the blocks, formatting volume, etc.
* Simplicity of file storage makes it a great solution for sharing a large number of files and folders within an organization.
* Use cases 
  * Documents, images, audio, and video files are stored in blobs.
* Software
  * Cloud Agnostic: 
  * AWS:  Amazon Elastic File System (EFS)
  * Azure: Azure Files
  * GCP: Google Filestore

### Storage - Block
* Common storage devices like hard disk drives (HDD) and solid-state drives (SSD) that are physically attached to servers
* Block storage presents the raw blocks to the server as a volume. 
* Most flexible and versatile form of storage. 
* The server can format the raw blocks and use them as a file system, or it can hand control of those blocks to an application. 
  * Some applications like a database or a virtual machine engine manage these blocks directly in order to squeeze every drop of performance out of them.
* Block storage is not limited to physically attached storage. 
* Block storage could be connected to a server over a high-speed network or over industry-standard connectivity protocols like Fibre Channel (FC) and iSCSI. 
* Conceptually, the network-attached block storage still presents raw blocks. 
* To the servers, it works the same as physically attached block storage. 
* Whether to a network or physically attached, block storage is fully owned by a single server. 
  * It is not a shared resource.
* Software
  * Cloud Agnostic: Hadoop distributed file system(HDFS)
  * AWS: Amazon Elastic Block Store (EBS)
  * Azure: Azure Disks
  * GCP: Persistent disks

### Storage - Object
* Tradeoff to sacrifice performance for high durability, vast scale, and low cost.
* Stores all data as objects in a flat structure.
* No hierarchical directory structure.
* Data access is normally provided via a RESTful API.
* Use case:
  * relatively “cold” data and is mainly used for archival and backup.
* Software
  * Cloud Agnostic: MinIO
  * AWS: AWS S3
  * Azure: Azure blob storage
  * GCP: Google block storage, Google Cloud storage

### Storage - Data warehouse
* Purpose: Analyze aggregated historical data from OLTP applications
  * OLAP applications need datastores that support high throughput reads on a large number of (read-only) records.
  * OLAP applications need an optimized column-read operation on a table.
  * Reporting needs can be met with data warehouse solution
* Software:
  * Cloud Agnostic:  Kudu
  * Commercial: Snowflake, Terradata
  * AWS: Redshift
  * Azure: Azure Synapse
  * GCP: Bigquery (serverless)

### Storage - Data lake
* Has all kinds of data dumped
* perform aggregations or run machine learning algorithms.
* Hadoop as storage of all the data
* Software
  * Cloud Agnostic: Databricks, Dremio, Hadoop distributed file system(HDFS), Vertica
  * AWS: S3
  * Azure: Azure Data Lake Storage (ADLS)
  * GCP: Google cloud storage (GCS)

### Storage - Streaming SQL
* Database that runs SQL queries continuously on streams, incrementally storing results in tables.
* Software
  * Open source: ksqlDB, StreamCQL, pipelinedb, squall, Materialize, Siddhi
  * Enterprise: 
  * AWS: 
  * Azure: 
  * GCP: 

#### Data ingestion - Message Queue
* Multiple producer, single consumer
* Stores the message temporarily in the queue
* Whenever the message is polled from the queue, it is gone.
* Delay or cancel message delivery
* No ordering guarantees
* Use cases: Long running/resource hungry requests queuing, async messages,
* Software
  * Cloud Agnostic: RabbitMQ, ActiveMQ
  * AWS: Amazon SQS
  * Azure:
  * GCP: Cloud Tasks, Cloud Pub/Sub

#### Data ingestion - Notification service
* Multiple publishers, multiple subscribers
* Fan-out/send notification to a set of subscribers subscribed to a topic
* Ephemeral data
* No queues
* Software
  * Cloud Agnostic:
  * AWS: Amazon SNS
  * Azure:
  * GCP: Firebase Cloud Messaging

#### Data ingestion - Publisher-Subscriber
* Much useful for fanout i.e. multiple publisher/subscriber
* large amounts of throughput
* pipes are persistent
* Stream and Batch-processing
* Retry and Dead-letter queue
* Replay (undo-ing ACKs) possible for most of the pub/subs
* Kafka & Amazon Kinesis
  * Checkpointing: Continue from a particular offset i.e. checkpoint when a consumer dies.
  * Long polling by the subscriber to receive messages. There is a slight delays.
  * Scaled by increasing partitions
* Google pub-sub & RabbitMQ
  * Subscription have a separate copy of the queued messages
  * Subscription copy is deleted when an ack is received from subscriber.
  * Messages can either be pulled by/pushed to subscriber from the subscription copy.
  * At-least once delivery
  * Best effort ordering
  * Publisher: choose between batching vs streaming for better throughput vs latency
  * RabbitMQ establishes persistent channels to send notifications to subscribers. It is two-way.
* Delayed Queues
  * Kafka does not have the ability to delay queues. SQS does.
* Push vs Pull
  * Push: RabbitMQ, Google pub/sub
  * Pull: Kafka (batch of messages), Google pub/sub
* Use cases: Event logs
* Software
  * Cloud Agnostic: Kafka, Rabbit MQ, Apache Pulsar(Yahoo), CloudEvents, NATS
  * AWS: Amazon Kinesis
  * Azure:
  * GCP: Google Pub/Sub

### Data ingestion - Change data capture
* Capture change streams from SQL databases
* Software
  * Commercial:
  * OpenSource: 
  * AWS: 
  * Azure:
  * GCP: Datastream (Serverless)

### Data processing - Batch
* Data collected in bulk, would be processed in batches.
* Has access to all data
* Might compute something big and complex
* Is generally more concerned with throughput than latency of individual components of the computation
* Has latency measured in minutes or more
* Also compute on continuous data with a window size of one day.
* Mapreduce Algorithm
  * Mapper: written by user. Maps input to an output
  * Shuffle: performed by hadoop. Shuffle the input in a way easier for the reducer
  * reducer: reduces the values to a single value i.e. perform aggregation
* Use case:
  * Payroll processes, Line item invoices, Supply chain and fulfillment
  * Message classification, user classification
* Software
  * Commercial:  
  * OpenSource: Spark, Hive(Hadoop data), Apache Bean(Definition language), Dbt
    * Spring Cloud Data Flow
  * AWS: Glue
  * Azure: 
  * GCP: Dataflow (Serverless), Cloud dataproc (Managed Hadoop + Spark, Serverless)

### Data processing - Stream
* Process continuous data to provide low-latency analytics.
  * Can be performed on historical or real-time data.
* Analyzing streaming cross-device data in near real-time
* Computes a function of one data element, or a smallish window of recent data
* Encompasses operations on and/or using individual messages as well as 
  * operations on collection of messages as they flow into the system.
* Needs to complete each computation in near-real-time — probably seconds at most
* Computations are generally independent
* Asynchronous – source of data doesn’t interact with the stream processing directly, like by waiting for an answer
* Use cases: ATMs, Air traffic control, Anti-lock braking systems in your car
* Software
  * Open Source Streaming Engine: Apache storm, S4, Apache Flink, Apache Samza (LinkedIn), Spring Cloud Data Flow
  * Open source Library: Kafka streams (Java library), Faust (Python Library)
  * Stream DSL: Apache Bean(Definition language)
  * AWS: AWS Kinesis Data Analysis(Apache Flink)
  * Azure: Azure Stream Analytics
  * GCP: Dataflow
  * IBM: IBM Streams

### Data Integration - ETL/ELT
* ETL is the process of taking database data and loading in datawarehouse solutions.
* ETL is outdated as extraction is not required any more.
  * Data ingestion is owned by the team which owns the data. These days, they use pub-sub to ingest data.
* Software
  * Commercial: Fivetran, Talend, Informatica
  * Open source: Airbyte, Meltano
  * AWS:
  * Azure:
  * GCP: Cloud datafusion

### Data Integration - Reverse ETL
* Reverse ETL is the process of copying data from a central data warehouse to operational systems of record, including but not limited to SaaS tools 
* Use case: growth, marketing, sales, and support
* Software
  * Commercial: Census, Hightouch
  * Open source: Grouparoo
  * AWS:
  * Azure:
  * GCP:

### Analytics - Data Cataloging
* Unified view of all datasets
* Simple and searchable keyword search.
* Real pre-built tag templates for tagging data assets.
* Integrated auto-tagging for sensitive data in Bigquery powered by Data Loss Prevention (DLP)
* Software
  * Open Source: Amundsen, Datahub
  * Enterprise: Alation, Atlan, Collibra
  * AWS: 
  * Azure:
  * GCP: Data catalog

### Analytics - Query Engine
* Software
  * Cloud Agnostic: Presto, Trino, Apache Drill
  * AWS: Athena (Managed Presto)
  * Azure: 
  * GCP: Big query 

### Analytics - Visualization - Business intelligence
* Software applications used to analyze an organization’s raw data.
* Software
  * Open source:  Apache Superset, Metabase, Jupyter
  * Commercial: Looker, Tableau, Hubspot, Thoughtspot, Zoho, Freshworks, Preset
  * AWS:
  * Azure:
  * GCP:

### Analytics - Visualization - Operational intelligence
* Real-time dynamic, business analytics that delivers visibility and insight into data, streaming events and business operations.
* Software
  * Open source: 
  * Commercial: Netspring, Observe
  * AWS:
  * Azure:
  * GCP:

