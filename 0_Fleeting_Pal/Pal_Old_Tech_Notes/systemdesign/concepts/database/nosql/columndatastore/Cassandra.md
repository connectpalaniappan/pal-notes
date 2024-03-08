
### Characteristic
* No master slave
* No separate config server
* Data is replicated across nodes
* Different nodes, data centers, geographies
* Eventually consistent

### Cassandra Query Language - CQL

#### Help

#### Describe
* ```DESCRIBE CLUSTER```
* ```DESCRIBE KEYSPACES```

#### SHOW
* ```SHOW VERSION```

#### CREATE
```
CREATE KEYSPACE mykeyspace WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1};
```

```
USE mykeyspace; 
CREATE TABLE person(first_name text, last_name text, id text, PRIMARY KEY (id));
DESCRIBE TABLE person;
INSERT INTO person (first_name, last_name, id) VALUES ('Pal', 'Mei', '1');
INSERT INTO person (first_name, last_name, id) VALUES ('Foo', 'Bar', '2');
SELECT * FROM person;

//works, because id is the primary key
SELECT * FROM person WHERE id = '1'; 

// throws an error because of performance impacts
SELECT * FROM person WHERE first_name = 'koushik'; 

// works and updates the existing row
INSERT INTO person (first_name, last_name, id) VALUES ('Foo1', 'Bar1', '2'); 

// works based on the primary key
DELETE FROM person WHERE id='2';

// DELETE all rows
TRUNCATE person;

// DROP TABLE person;
```





