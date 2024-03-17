# NoSQL datastores

### Characteristic
- Data can be unstructured, distributed
  - Schema can be dynamic
  - Queries are focussed on a collection of documents (Unstructured Query Language)
- Basically available, Soft state, eventually consistent (BASE)  
  - performance and scalability
- Easier to scale horizontally.
  - Easier to store large volumes of data. 
  - Reduces the cost to scale faster as it can be scaled on cheaper machines in-house and on cloud.
- Useful for rapid development. 

### Types

| Database | Type | partition - consistency vs availability | No partition - consistency vs low latency | Hashing | Use case |
| :---        |    :----:   |          ---: | ---: | ---: | ---: |
| Redis | Key-value store | Consistency | | | Cache| 
| Memcached | Key-value store | Consistency | | | Cache|
| Voldermont | Key-value store | Availability | | | Shopping basket|
| Dynamo   | Key-value store | Availability | Low latency| Consistent Hashing | Order History|
| Riak   | Key-value store | Availability | Low latency| | Shopping basket, Big data|
| MongoDB | Document datastore | Consistency | Consistency | | Order history, Website, Social network, Big data |
| CouchDB | Document datastore | Consistency | Low latency or Consistent | | Order history, Website |
| RethinkDB | Document datastore | | | | Social network |
| HBase/ Hadoop/HStore | Wide column datastore | Consistency| Consistency | | Order history, Social network, Big data |
| Bigtable | Wide column datastore | Consistency| Consistency |||
| Volt | | Consistency| Consistency |||
| Cassandra | Wide column datastore | Availability | Low latency | Consistency Hashing| Shopping basket|
| MapR | Wide column datastore |||||
| Neo4j | Graph database | Consistency ||| OLTP |
| InfiniteGraph | Graph database |||||
| Yahoo Pnuts | | Consistency | Low latency |||
