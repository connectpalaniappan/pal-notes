# SQL database

## Characteristic 
- Data needs to be structured.
  - Schema is almost static and pre-defined.
  - Structured query language
- Atomicity, Consistency, Isolation and durability (ACID) 
  - Data reliability and safe guarantees
- Easier to scale vertically.
- In theory, RDBMS is consistent and available with a master-slave architecture.
In case of any failures i.e. partition tolerance, system can satisfy either being consistent or being available.

### Row Id
* Internal and system maintained
* In certain databases, it is the same as primary key 
  * but other databases like Postgres have a system column row_id (tuple_id)

### Page
* Depending on the storage model(rows vs column store), the rows are stored and read in logical pages
* the database does not read a single row, it reads a page or more in a singleIO and we get a lot of rows in the IO.
* Each page has a size (e.g 8KB in PostGres, 16KB in mySQL)
* Assume each page holds 3 rows, with 1001 rows you will have 1001/3 ~= 333 pages

### IO 
* IO operation (input/output) is a read request to the disk
* we try to minimize this as much as possible
* An IO fetch 1 page or more depending on the disk partitions and other factors.
* An IO cannot read a single row, its a page with many rows in them, you get them for free.
* You want to minimize the number of IOs as they are expensive.
* Some IOs goes to the operating system cache and not the disk.

### Heap
* The heap is the data structure where the table is stored with all its pages one after another
* This is where the actual data is stored including everything.
* Traversing the heap is expensive as we need to read so may data to find what we want.
* That is why we need indexes that help tell exactly what part of the heap we want to read.
  * what pages of the heap we need to pull.

### Index
* An index is another data structure separate from heap that has pointers to the heap
* It has part of the data and used to quickly search for something.
* You can index on one column or more.
* Once you find a value of the index, you go to the heap to fetch more information.
* Index tells you EXACTLY which page to fetch in the heap instead of taking the hit to scan every page in the heap.
* The index is stored as pages and cost IO to pull the entries of the index.
* The smaller the index, the more it can fit in the memory the faster the search
* Popular data structure for index is B-trees
* Sometimes heap table an be organized around a single index.
  * This is called the clustered index or an index organized table
* Primary key is usually a clustered index unless otherwise specified.
* MySQL InnoDB always has a primary key (clustered index) 
  * other indexes point to the primary key value
* PostGres only have secondary indexes and all indexes point directly to the row_id which lives in the heap.

### Offset, Limit
* Don't use offset due to performance problems
  * offset 1000 limit 100 would read all the first 1100 rows and drop the first 1000 rows
  * New rows can be added leading to duplicate reads.
* Better to replace filter with a column condition
  * Fetch all the rows with id greater than 10.

### Query plan
* `EXPLAIN ANALYSE`

### Connection pooling
* Max Connections: Number of maximum connections to establish
* Connection timeout: Max time it can take to establish a connection. 0 for infinite time.
* Idle timeout: Max time to wait before it takes to get rid of an idle connection. 

### Transaction 
* Collection of queries hat are treated as a single unit to a fork.
* Even when you don't mention transaction, 
  * database creates a transaction internally
  * executes the query
  * applies auto-commit.
* Change and modify data
* Read data
  * Example: Generate a report and get consistent snapshot based at the time of transaction.
* `BEGIN TRANSACTION`
  * `BEGIN TRANSACTION ISOLATION LEVEL REPEATABLE READ`
* `COMMIT`
* `ROLLBACK`
  * Unexpected ending would also be rollback-ed

## PostGreSQL
## MySQL
## MariaDB
## MS SQL
## Oracle
## SQLLite