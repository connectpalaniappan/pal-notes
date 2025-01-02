identity:: #Architect
archetype:: #giver
year:: [[future]],[[2022]],[[2023]],[[2024]],[[2025]]
document:: #Area
status:: #todo

-
-
-
- Projects
	- Architecture guild
	  collapsed:: true
		- Year end review
		  collapsed:: true
			- 2024
			  collapsed:: true
				- **Active Architecture Guild Participation:** Consistently reviewed key project architectures, providing valuable feedback and ensuring alignment with company standards.
				- **Influential Leadership:** Actively participated in Architecture Guild meetings, guiding discussions and helping steer key initiatives in the right direction.
				- **Strategic Vision:** Played a crucial role in setting the architectural trajectory for company projects, impacting technology choices and development practices.
				- **Cross-Team Collaboration:** Fostered collaboration between onDot and Clover teams by facilitating connections and identifying relevant stakeholders for joint initiatives.
				- **Technical Expertise:** Leveraged deep technical expertise to provide guidance and recommendations on complex architectural challenges.
				- **Mentorship & Knowledge Sharing:** Mentored other engineers on architectural best practices and design principles, contributing to their professional growth.
				- **Process Improvement:** Contributed to the improvement of architectural review processes, enhancing efficiency and effectiveness.
				- **Problem Solving:** Successfully navigated challenging architectural discussions, finding solutions that balanced technical needs with business requirements.
		- Tasks
			- TODO [#B] Eric document on saving timestamp review
			- TODO [#B] Review Push decomposition by Rishab https://github.corp.clover.com/clover/architecture/pull/110/files
	- Platform abstraction
	- Cloud platform oncall
	  collapsed:: true
		-
	- ChatBot AI
	  collapsed:: true
		- Tasks
		  collapsed:: true
			- DONE [#B] Find out what type of task to give to #Krishna #Ramya #Priya 
			  DEADLINE: <2024-12-09 Mon>
		- Year end review
		  collapsed:: true
			- 2024
			  collapsed:: true
				- **Successfully created embeddings from wiki documents:** This lays the foundation for the chatbot to understand and retrieve relevant information from the knowledge base.
				- **Enabled accurate query responses using a Large Language Model (LLM):** The chatbot can now effectively process user questions and provide helpful answers based on the information embedded from the wiki docs.
				- **Collaboration with Ramya:** Provided essential support to Ramya in achieving these milestones, demonstrating teamwork and contributing to the project's success.
				- **Next Steps: Streamlit Integration:** The focus is now shifting towards integrating the chatbot with Streamlit. This will involve deploying the chatbot as a cloud function and linking it to Streamlit within Omnibot updates. This will make the chatbot accessible and user-friendly.
				- **Phase 1 Completion:** The successful completion of embedding creation and LLM integration marks a significant milestone in the chatbot AI project. This sets the stage for further development and enhancement in the upcoming phases.
	- Capability Authorization
	- COS guideline
	  collapsed:: true
		- TODO [#A] COS guideline project complete
	- COS oncall
	  collapsed:: true
		- Year end review
			- 2024
			  collapsed:: true
				- **Leadership & Responsibilities**
				- **Defined Roles:** Clearly define roles and responsibilities for each engineer on the on-call rotation. This could include specialization in certain areas of the COS monolith or specific tasks like incident response, triage, and communication.
				- **Mentorship:** Encourage engineers to mentor less experienced team members to improve their skills and confidence in handling incidents.
				- **Weekly training meeting:** Provided engineers with training from other infra and product teams to understand and improve the overall handling of COS outages.
				  
				  **Runbook Optimization**
				- **Comprehensive Documentation:** Ensure your COS runbook is thorough and up-to-date. It should include:
					- Common error messages and their solutions
					- Step-by-step guides for troubleshooting frequent issues
					- Escalation procedures for complex problems
					- Contact information for relevant teams
				- **Easy Access:** Make the runbook easily accessible to the on-call team (e.g., a central knowledge base, a dedicated Slack channel).
				- **Continuous Improvement:** Regularly review and update the runbook based on new incidents and feedback from the on-call team.
				  
				  **Effective Weekly Meetings**
				- **Incident Review:** Dedicate time during weekly meetings to discuss recent incidents, identify root causes, and document solutions in the runbook.
				- **Knowledge Sharing:** Encourage staff engineers to share their experiences, tips, and best practices related to on-call duty and the COS monolith.
				- **Proactive Problem Solving:** Use the meetings to brainstorm potential issues, identify areas for improvement in the COS system, and proactively prevent future incidents.
				- **Feedback and Communication:** Create an open forum for feedback on the on-call process, the runbook, and any challenges faced by the team.
				  
				  **Beyond the Basics**
				- **On-Call Tools:** Explore using on-call management tools to streamline scheduling, alerting, and communication.
				- **Postmortems:** For major incidents, conduct more detailed postmortems to analyze the incident's impact, timeline, and contributing factors. This can lead to more significant system improvements and prevent similar incidents in the future.
				- **Automation:** Identify opportunities to automate tasks and processes within the COS monolith to reduce manual intervention and the risk of human error.
	- COS oncall training
	  collapsed:: true
		- TODO [#B] Performance testing by Swaraj documentation
		- TODO [#B] Write a runbook to debug capability issues https://cloverpos.slack.com/archives/G01J0R3D5BN/p1732652887673679
	- COS observability
	- COS authtoken deletion
	  collapsed:: true
		- TODO [#A] I was wondering if you could look over [https://github.corp.clover.com/clover/server/pull/17774/files](https://github.corp.clover.com/clover/server/pull/17774/files) for me with a critical eye. I am concerned that I may have been too aggressive in what is a token read. I have commented on the lines I am concerned about.
		  DEADLINE: <2024-12-10 Tue>
	- Ondemand project
	  collapsed:: true
		- **Ondemand Project:** Provided key technical guidance to SRE team that accelerated the Ondemand project's successful launch.
		- **Capability Decomposition:** Guided the capability decomposition effort, leading to a more modular and maintainable architecture.
		- **MySQL 8 upgrade:** Facilitated a smooth transition to MySQL 8 by providing the needed details to Ramya, improving database performance and reliability.
		- **k8sgateway Alerts:** Worked with CPE folks to optimize k8sgateway alerts, enabling faster incident response and minimizing downtime.
		- **Developer App Rate Limit Improvements:** Worked with Developer portal team to identify effective rate limiting for developer apps, preventing abuse and ensuring service availability.
		- **Cloud Platform Onboarding:** Onboarded multiple folks to Cloud platform team. Now have organized the library for future onboarding.
		- **COSoncall Outages:** Provided critical support during COSoncall outages, minimizing downtime and ensuring service continuity.
		- **Datascience Cloud AI Chatbot:** Supported Datascience team to address merchant-facing Cloud AI chatbot challenges, enhancing the customer experience.
		- **Cloud Platform Oncall Support:** Offered expert support via Cloud Platform Oncall, resolving issues.
		- **100 Day Project Goals:** Provided support to OnDot team to inter-service communication for the Appointment k8s service, resulting in delivering their product on time.
	- COS reliability
	  collapsed:: true
		- Year end review
			- 2024
			  collapsed:: true
				- Review
				  collapsed:: true
					- **Improved Fault Tolerance:**
						- **Bulkheading:** Introduced bulkheads to limit resource usage and prevent one service from consuming all available resources. (COS-113)
					- **Optimized Resource Management:**
						- **Improve resource:** Optimize CPU, thread and disk utilization. (COS-93, COS-95, COS-67)
						- **Load Balancing:** Utilized load balancing to distribute traffic evenly across servers. (COS-165)
						- **Sharding & Partitioning:** Optimized adding and need to optimize remove shard to distribute data and improve performance. (COS-65, COS-109, COS-129, COS-131)
					- **Minimized Manual Intervention:**
						- **Auto Remediation:** Developed auto-remediation mechanisms to automatically address common issues. (COS-118)
						- **Avoid Manual Restarts:** Minimized the need for manual restarts through automation. (COS-103)
					- **Enhanced Performance & Efficiency:**
						- **Caching:** Work with CORESERV team to optimize caching for read and write operations to improve response times. (COS-85, CORESERV-1253, CORESERV-1592, SRE-7233)
						- **Optimization:** Conducted profiling and optimization to identify and address performance bottlenecks. (COS-6, COS-57, COS-71)
					- **Improved Error Handling & Resilience:**
						- **Unblocking HTTP Requests:** Optimized request handling to prevent blocking and improve throughput. (COS-58, COS-199, COS-208, COS-207, COS-206, COS-205)
						- **Timeout & Fallback:** Implemented timeouts and fallbacks to handle failures gracefully. (COS-54, COS-101)
						- **Proper Error Handling:** Ensured comprehensive error handling to capture and address issues effectively. (COS-119)
					- **Increased Observability:**
						- **Metrics, Logs, Tracing:** Collected and analyzed metrics, logs, and traces to gain insights into system behavior. (COS-2, COS-24, CPE-2660)
						- **Alerts:** Set up alerts to notify on critical events and potential issues. (COS-1)
					- **Controlled Rollouts & Feature Management:**
						- **Disable via Feature Flags:** Enabled the ability to disable features via feature flags for controlled rollouts and testing.
					- **Traffic Management:**
						- **Rate Limiting:** Introduced rate limiting to control traffic flow and prevent abuse. (COS-69, COS-87, COS-180, DP-7414)
				- Task breakdown note
				  collapsed:: true
					- **Enhancing COS Reliability**
					- **Improved Fault Tolerance:**
						- **Circuit Breakers:** Implemented circuit breakers to prevent cascading failures and isolate faulty services. (COS-2, COS-1, COS-174)
						- **Bulkheading:** Introduced bulkheads to limit resource usage and prevent one service from consuming all available resources. (COS-113)
						- **Rolling Restarts:** Enabled rolling restarts to minimize downtime during deployments and updates.
						- **Disaster Recovery:**  Established disaster recovery procedures to ensure business continuity in case of catastrophic events.
					- **Optimized Resource Management:**
						- **Automatic Scaling:** Implemented automatic scaling to dynamically adjust resources based on demand. (COS-93, COS-95)
						- **Load Balancing:** Utilized load balancing to distribute traffic evenly across servers. (COS-165)
						- **Queueing:** Introduced queues to handle traffic spikes and prevent overload. (COS-67)
						- **Sharding & Partitioning:**  Implemented sharding and partitioning to distribute data and improve performance. (COS-65, COS-109, COS-129, COS-131)
						- **Horizontal & Vertical Scaling:** Enabled both horizontal and vertical scaling to adapt to changing needs.
					- **Minimized Manual Intervention:**
						- **Auto Remediation:**  Developed auto-remediation mechanisms to automatically address common issues. (COS-118)
						- **Automatic Restarts:** Configured automatic restarts for failed services.
						- **Avoid Manual Restarts:** Minimized the need for manual restarts through automation. (COS-103)
					- **Enhanced Performance & Efficiency:**
						- **Caching:** Implemented caching for read and write operations to improve response times. (COS-85, CORESERV-1253, CORESERV-1592, SRE-7233, COS-121)
						- **Asynchronous Processing:** Introduced asynchronous processing to improve responsiveness and throughput.
						- **Optimization:** Conducted profiling and optimization to identify and address performance bottlenecks. (COS-6, COS-57, COS-71)
					- **Improved Error Handling & Resilience:**
						- **Transaction Processing:**  Ensured reliable transaction processing with compensation transactions and reverse transactions.
						- **Unblocking HTTP Requests:**  Optimized request handling to prevent blocking and improve throughput. (COS-58, COS-199, COS-208, COS-207, COS-206, COS-205)
						- **Timeout & Fallback:** Implemented timeouts and fallbacks to handle failures gracefully. (COS-54, COS-101)
						- **Default Values & Available Data Sources:** Utilized default values and alternative data sources to provide fallback mechanisms.
						- **Proper Error Handling:**  Ensured comprehensive error handling to capture and address issues effectively. (COS-119)
					- **Increased Observability:**
						- **Metrics, Logs, Tracing:** Collected and analyzed metrics, logs, and traces to gain insights into system behavior. (COS-2, COS-24, CPE-2660)
						- **Alerts:** Set up alerts to notify on critical events and potential issues. (COS-1, COS-26)
					- **Controlled Rollouts & Feature Management:**
						- **Disable via Feature Flags:**  Enabled the ability to disable features via feature flags for controlled rollouts and testing.
					- **Traffic Management:**
						- **Backpressure:** Implemented backpressure mechanisms to prevent overload and ensure stability.
						- **Rate Limiting:** Introduced rate limiting to control traffic flow and prevent abuse. (COS-69, COS-87, COS-180, DP-7414)
					- **Code & Design Best Practices:**
						- **Functional Decomposition:**  Applied functional decomposition to break down complex systems into smaller, more manageable components.
				- Thank you note
				  collapsed:: true
					- "I'm incredibly proud of the monumental improvements we've achieved in COS reliability! It's been a challenging but rewarding journey, and the results are truly amazing.  Big thanks to Priya for setting up that initial meeting with Tatsuro, Loki, and Noel - their insights and support were invaluable.  We've tackled complex issues, implemented innovative solutions, and significantly boosted COS stability and performance.  Tatsuro and Loki, your appreciation for this work means a lot!  This success is a testament to our collective efforts and dedication."
	- MySQL 8 upgrade
	  collapsed:: true
		- Year end review
			-
- People
	- Vinayak
	  collapsed:: true
		- [[2024-12-10 Tuesday]]
		  collapsed:: true
			- Sharding is enabled in LA
			- Multiple auth nodes
			- Need the optimizations
			- COS decomposition
			  collapsed:: true
				- Pull everything out i.e. inventory,
				- Auth server separate the code layer alone
			- Fiserv gateway: combine the IPG,
	- Priya 1-on-1
	  collapsed:: true
		- [[2024-12-13 Friday]]
		  collapsed:: true
			- Lost clover culture
			- Platform abstraction update
				- Meeting with Fabio
				- Presented to Vinayak
	- Tatsuro
	  collapsed:: true
		- 2024 Review
	- Ramya
	  collapsed:: true
		- 2024 Review
	- Karan
	  collapsed:: true
		- 2024 Review
	- Krishna
- Week Planning
	- Mon - Incident retrospective, Architecture review, Architecture working group (Already know; Urgent and important)
	- Tue - Coding on short term problems (Already know; Urgent and not important; try to delegate)
	- Wed - Explore solutions to address problems, Scalability work (New; Not urgent and important)
	- Thur - Coding to address long term problems (New; Not urgent and important)
	- Fri - Sprint planning, Sprint demos, Architecture reading (Sharing knowledge; Not urgent and important)
-
- ## Discussions
	- [ ] Also brainstorm on how to migrate all microservices into K8s DR clusters in bulk after batch 1 is completed successfully. What is batch 1?
- ## Action items
- High impact items
	- Observability of COS did have a huge impact
- Document Changal presentation on how prometheus is setup in Clover
- Remote debugging possible in dev environments?
-
-
-
-
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