## Notification service


### Source
* Push Notifications to million devices https://youtu.be/6w6E_B55p0E 

### Functional Requirements
* Near real time sync notification

* Notifications to devices - fan out
* User notification preference
* In-app notifications - persistence
* Notifications aggregation - dedupe notifications
* Notification decider - not to bombard user with notifications

### Non functional requirements


### Components

#### Services
* Push Consumer 
* Push Fanout
  * Notification fan-out
    * Send to multiple devices which belong to the same user
      * Identify this from the device service
    * check the notification preference
    * create a task and delegate it to publisher
    * responsibility
      * does this event deserve a notification?
      * does this user require a notification? 
  * Notification aggregation
    * LinkedIn: One notification per object, keep updating itself
    * Instagram: Notification of same type and object are aggregated and grouped.
  * Notification preference
    * max notifications per day
    * lesser affinity
    * configured preference
  * Priority classification
    * Have different queues for priority
    * SLA for P0 queue is less than 5 seconds
* Push Publisher
  * Heavy on network I/O. Use a lot of network cards.
  * No database dependencies.
  * E.g. Email, phone, subscription ARN, body, etc.

#### Database 
* Notification persistence
  * Database: Bulk writes for notification
  * No joins with other data. So better to use NoSQL
  * DynamoDB

#### Eventing System
* Real time sync notification
  * Event bus: Sending notifications
  * Kafka or kinesis
  * Scale depends on the partition
    * One consumer would consume from one partition
    * For 10 partitions, you cannot have 50 consumers

#### Client   
* Miscellaneous
  * Keep the client dumb
  * Easier to deploy backend system multiple times
