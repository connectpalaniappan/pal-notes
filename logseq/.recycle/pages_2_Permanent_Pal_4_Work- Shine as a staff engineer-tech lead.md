---
Created: 2024-01-31T11:04
AssignedTo: palaniappan meiyappan
Target Completion Date: 2024-07-31
Completed: false
Next task Date: 2024-02-02
Type: TASK
---

- ## Week Planning
  
  Mon - Incident retrospective, Architecture review, Architecture working group (Already know; Urgent and important)
  Tue - Coding on short term problems (Already know; Urgent and not important; try to delegate)
  Wed - Explore solutions to address problems, Scalability work (New; Not urgent and important)
  Thur - Coding to address long term problems (New; Not urgent and important)
  Fri - Sprint planning, Sprint demos, Architecture reading (Sharing knowledge; Not urgent and important)
- ## Discussions
- [ ] Also brainstorm on how to migrate all microservices into K8s DR clusters in bulk after batch 1 is completed successfully. What is batch 1?
- ## Action items
- High impact items
	- Observability of COS did have a huge impact
- Document Changal presentation on how prometheus is setup in Clover
- Remote debugging possible in dev environments?
- Open source contribution
- Speak in a conference
- Conduct a webinar
- File a patent
- ## Analysis
- ### Memcache failure findings 
  
  Memcache node failure [https://clovernetwork.grafana.net/goto/MVYr6CJIR?orgId=1](https://clovernetwork.grafana.net/goto/MVYr6CJIR?orgId=1) . From machines `message` log, 
  1. `30:48` there was a puppet run 
  2. `32:xx` bad state was around; no metrics from memcache 
  3. `37:44` Google rebooted the node at  physically.
  4. `37:xx` recovered from bad state 
  5. `38:02` node rebooted 
  6. `39:xx` metrics flowed from memcached 
  2. We now block on a very common flow (this seems new) 
  3. the node was not down, but in a degraded mode which could amplify the timeout/offline status.
  1. only thing I can think off is that the "bad" node did not fail completely.. but for some time became unresponsive. ie.. it was visible, but did not react. That way COS still "see" the node and keep on retrying.
  4. <mark style="background: #FF5582A6;">How does redistribute failure reason work?</mark> 
  1. <mark style="background: #BBFABBA6;">Move on to functional nodes when nodes fail.
  2. In this failure mode, the failure of a node will cause its current queue and future requests to move to the next logical node in the cluster for a given key.
  3. this operation will fallback to database on failure? </mark>
  5. <mark style="background: #FF5582A6;">How does cancel failure reason work? </mark>
  1. <mark style="background: #BBFABBA6;">Automatically cancel all operations heading towards a downed node. 
  2. this operation will fallback to database on failure </mark>
  6. <mark style="background: #FF5582A6;">How does retry failure reason work? </mark>
  1. <mark style="background: #BBFABBA6;">Continue to retry a failing node until it comes back up. </mark>
  2. <mark style="background: #BBFABBA6;">This failure mode is appropriate when you have a rare short downtime of a memcached node that will be back quickly, and your app is written to not wait very long for async command completion.</mark>
  3. <mark style="background: #BBFABBA6;">this operation will fallback to database on failure </mark>
  7. <mark style="background: #BBFABBA6;"><mark style="background: #FF5582A6;">How does fallback happen to database? </mark></mark>
  1. <mark style="background: #BBFABBA6;">Fail to get the data from memcache </mark>
  2. <mark style="background: #BBFABBA6;">Lookup database on failure </mark>
  3. <mark style="background: #BBFABBA6;"> Whenever a cache is missed, it loads the data from database and sets it in memcache () </mark>
  8. <mark style="background: #FF5582A6;">How does memcache health check work? </mark>
  1. 
  9. 95% requests failed 
  1. `477` requests over `2000`ms sustained, the rest just error due to queue buildup. [https://clovernetwork.grafana.net/goto/JB6Zk3JSR?orgId=1](https://clovernetwork.grafana.net/goto/JB6Zk3JSR?orgId=1) 
  2.  <mark style="background: #FF5582A6;">wonder what tx those `477` are? </mark>
  3. https://clovernetwork.grafana.net/goto/L1vKeCJIg?orgId=1 HAProxy metrics 
  10. Dedupe 
  1. https://clovernetwork.grafana.net/goto/JB6Zk3JSR?orgId=1 <mark style="background: #FF5582A6;">why are we doing dedupe in memcache? not in redis, right?</mark> 
  1. Move to memcache was done in 2016/17 
  2. <mark style="background: #FF5582A6;">why are we doing a set expire on a line_item update (!?) for dedupe... ?</mark>
  1. 
  3. <mark style="background: #FF5582A6;">why would we store a value in memcache on a line_item update to an order?</mark> 
  11. Analysis 
  1. <mark style="background: #FF5582A6;">Try to stop memcache in lower environments and see the impact?</mark> 
  12. Improvements
  1. Ticket to lower memcache timeouts 
  2. Need to change the failover mechanism? 
  3. Discuss on breaking caches into functional groups 
  4. offloading the memcache lookup to a different executor to not block event executors
  
  Is it possible for a memcache node to pass health checks when called using spymemcache library client but not process any request? 
  > [!ai]+ AI
  >
  > Yes, it is possible for a memcache node to pass health checks when called using the spymemcache library client but not process any requests. This can happen due to various reasons, such as:
  > 1. **Network Issues**: The memcache node might be experiencing network problems, causing it to respond to health checks successfully but fail to process actual requests. This could be due to network congestion, firewall rules, or other network-related issues.
  > 2. **Resource Constraints**: If the memcache node is running out of resources, such as memory or CPU, it might still respond to health checks but struggle to handle actual requests. This can happen when the node is overloaded or experiencing high traffic.
  > 3. **Software Issues**: There could be bugs or issues in the memcache server software that cause it to behave unexpectedly. For example, a specific command or operation might trigger an error or cause the server to become unresponsive, while health checks that use different commands or operations might still work.
  > 4. **Configuration Problems**: Misconfigured memcache nodes or clients could lead to situations where health checks succeed, but requests fail. This could be due to incorrect settings, such as connection limits, timeouts, or other parameters.
  > 5. **Caching Layer Issues**: If the memcache node is part of a caching layer or distributed system, there might be issues with other components or dependencies that cause requests to fail, even though the memcache node itself appears healthy.
  > To troubleshoot such issues, you can try the following:
  > 1. **Check Network Connectivity**: Verify that there are no network-related problems between the client and the memcache node by running network diagnostic tools or checking firewall rules.
  > 2. **Monitor Resource Usage**: Monitor the memcache node's resource usage (CPU, memory, network) to identify any potential bottlenecks or resource constraints.
  > 3. **Analyze Logs**: Review the memcache server logs and client logs for any error messages or suspicious behavior that might provide clues about the issue.
  > 4. **Test with Different Clients**: Try using different memcache client libraries or tools to rule out any client-specific issues.
  > 5. **Verify Configuration**: Double-check the configuration of the memcache node and client to ensure that all settings are correct and consistent.
  > 6. **Investigate Dependencies**: If the memcache node is part of a larger system, investigate other components or dependencies that might be causing the issue.
  > By following these steps, you can identify and address the root cause of the issue, ensuring that the memcache node processes requests correctly and consistently.
  
  What are the steps performed by spymemcache library for memcache health checks? 
  > [!ai]+ AI
  >
  > The spymemcached library is a Python client for memcached, a distributed memory object caching system. It provides various features, including health checks for memcached servers. Here are the typical steps performed by the spymemcached library for memcached health checks:
  > 1. **Connection Pool**: The spymemcached library uses a connection pool to manage connections to memcached servers. The connection pool is initialized with a list of memcached server addresses and configurations.
  > 2. **Periodic Health Checks**: The library periodically performs health checks on the memcached servers in the connection pool. The frequency of these health checks can be configured.
  > 3. **Health Check Method**: The health check typically involves sending a simple command or request to the memcached server and checking for a valid response. The specific method used for the health check may vary based on the library version or configuration.
  > 4. **Server Status Tracking**: Based on the health check response, the library tracks the status of each memcached server as "alive" or "dead/failed". This information is maintained in the connection pool.
  > 5. **Connection Handling**: When a client application requests a connection from the connection pool, the library provides a connection to a "live" memcached server. If all servers are marked as "dead/failed", the library may retry the health checks or raise an exception, depending on the configuration.
  > 6. **Server Fail-over**: If a memcached server fails during operation, the library detects the failure through health checks or failed operations. It then marks the server as "dead/failed" and removes it from the active connection pool. Subsequent requests are directed to other "live" servers in the pool.
  > 7. **Server Recovery**: In some cases, the library may periodically attempt to reconnect to failed servers to check if they have recovered. If a previously failed server responds successfully to the health check, it can be marked as "alive" again and added back to the active connection pool.
  > 8. **Logging and Monitoring**: The spymemcached library typically provides logging and monitoring capabilities, allowing you to track the health status of memcached servers, connection pool statistics, and any errors or exceptions that occur during health checks or operations.
  > It's important to note that the specific implementation details and configuration options may vary depending on the version of the spymemcached library you are using. Additionally, some applications may implement custom health check mechanisms or use third-party monitoring tools in conjunction with the spymemcached library for more advanced monitoring and alerting capabilities.