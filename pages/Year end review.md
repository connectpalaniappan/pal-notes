- test
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
- ChatBot AI
  collapsed:: true
	- **Successfully created embeddings from wiki documents:** This lays the foundation for the chatbot to understand and retrieve relevant information from the knowledge base.
	- **Enabled accurate query responses using a Large Language Model (LLM):** The chatbot can now effectively process user questions and provide helpful answers based on the information embedded from the wiki docs.
	- **Collaboration with Ramya:** Provided essential support to Ramya in achieving these milestones, demonstrating teamwork and contributing to the project's success.
	- **Next Steps: Streamlit Integration:** The focus is now shifting towards integrating the chatbot with Streamlit. This will involve deploying the chatbot as a cloud function and linking it to Streamlit within Omnibot updates. This will make the chatbot accessible and user-friendly.
	- **Phase 1 Completion:** The successful completion of embedding creation and LLM integration marks a significant milestone in the chatbot AI project. This sets the stage for further development and enhancement in the upcoming phases.
- COS reliability
  collapsed:: true
	- Year end review
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
- COS oncall
  collapsed:: true
	- Year end review
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
	-
- COS authtoken deletion
	-
-
-
- ## Tasks
	- TODO [#B] Performance testing by Swaraj documentation
	- TODO [#B] Write a runbook to debug capability issues https://cloverpos.slack.com/archives/G01J0R3D5BN/p1732652887673679
-
- ## Tasks
- DONE [#B] Find out what type of task to give to #Krishna #Ramya #Priya 
  DEADLINE: <2024-12-09 Mon>
-
	-