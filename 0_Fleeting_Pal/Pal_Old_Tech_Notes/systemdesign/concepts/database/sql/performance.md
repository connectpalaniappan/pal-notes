
### Memory
* Provide sufficient memory to handle disk cache. 

### Avoid N+1 reads
* Assume a resource has N sub-resources.
* You should not query the database for N sub-resources and one main resource individually.
* All together you should be executing only two queries, one for main resource and all the sub-resources. 

### Indexes and how they work?
* Make a query with either the index or primary key. 
* Avoid joins
* Remove unnecessary columns
* Primary key can have more than one column. Change it to match based on how the query is constructed. 
* Let varchar max size be 255. MYSQL uses 255 + (1 character for length) to store in a byte. 
  Anything more than 255 characters would require extra bytes. 
* Avoid doing select *   

### Bloom filters
