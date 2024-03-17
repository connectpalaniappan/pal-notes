# Process the requirement
What we really mean when we say process requirements is “clarify” the question:

Many candidates forget to clarify the requirements. They jump in, finding they forgot an important goal. 
Other times, they fail to scope the problem, allowing their response to run too long, 
covering minutiae that the interviewer doesn’t care about. Both mistakes can result in rejection.



## functional requirements
* Users/Customers
  * Who is the user?
  * What different clients or devices do we need to support?
    * Would help us determine the load and storage.
    * Are we expected to design just the mobile application or other parts of the overall system too (e.g. API)?
    * Is it iOS or Android only, or cross-platform? Shall we support smartphones, tablets, both?
* Features to support
  * What are the goals or outcomes?
  * Do we need to support feature Y ?
  * What features should be left out?
  * Feature specific ?
    * What kind of data ie. text, image, audio, video are passed in API ?
    * Do we need to push any data to clients?
  * Any constraints to be aware of?
* System
  * Are we designing an MVP or final-product?
  * How big is the team who will implement and maintain our system?

### Common problems
* authentication/authorization
* reporting service

### Data problems
* Are we aggregating or storing data as individual events?
* How to make it extensible for data model changes in future?

### Computational problems
* First identify the clients/users who would be using the system
* Based on the users, identify the functionality they would need.
  * For example, to build an online video service, you might consider domain services that:
    * Videos: allow users to view, upload, or delete
    * Users: allow for creation, viewing, modification, or deletion
    * etc.

## non-functional requirements
* Availability vs Consistency
  * Available
    * Automatic failover 
    * load is evenly or randomly distributed
    * Fault tolerant - in case of failures, how would the system respond.
      * no single point of failure
      * How to recover data incase of an outage?
* Scalability
  * where we need to scale our system
  * Partition for faster processing
* Performance
  * how fast system should be
  * Have things in-memory and minimize disk reads.
* Durability
* Resiliency
  * Avoid data-loss, replicate data
* Security
* Cost
  * Design minimize the cost of development?
  * Design minimize the cost of maintenance?

### First principle thinking
1. scientific questioning of various preconceived statements
   1. Break the problem into fundamental pieces
   2. Build the solutions bottom-up
   3. Do not reason by analogy (Based on something which was done earlier)
   4. For example, everyone assumed electric cars are not feasible
      1. Tesla company broke the battery(problem) into smaller components
      2. Found each individual components are cheaper
      3. Learnt how to make a cheaper battery by combining all the smaller components.
  