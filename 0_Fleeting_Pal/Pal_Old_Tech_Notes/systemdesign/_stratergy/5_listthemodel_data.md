# Articulate the data model
This is about defining the database tables and the corresponding fields. If you defined the API well, then each service endpoint should be a corresponding DB table.
For example, lets design an video count service.

### SQL
* Defining nouns which are converted to tables
* Use foreign keys to reference related data.
* Data should be normalized
  * 
* Example: There should be a videos and channels table, among others.
  * From there, interviewers want you to specify the fields inside each table. 
  * videos fields: id, name, channel_id
  * channel fields: channel_id, name
  * video_stats fields: video_id, timestamp, count

### NO-SQL 
* Defining tables in terms of query execution
* Data can be denormalized
* Example: table would have all the following fields:
  * video_id, channel_name, video_name, 15:00, 16:00, 17:00 and so on.

## Discuss the trade-offs
* **Define data model**
    * Various system entities
    * How system entities would interact with each other
    * Data storage
    * Data transportation
    * Data encryption
    * Which database system would you use? SQL or NoSQL
    * Block storage system for storing photos and videos