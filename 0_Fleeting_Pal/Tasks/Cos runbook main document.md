---
tags:
 - nexus/note_log
 - people/pal
 - date/2024-05-16
---

---

## Alert Investigation 

1. Alert occurred 
2. Page primary COS on-call 
3. Start a discussion in #monolith-alerts-discussion 
	1. Click on emoji `monolith-error` to forward messages from other channel to #monolith-alerts-discussion channel 
4. [Impact analysis](#COSRunbook-ImpactAnalysis)
5. Yes: impact understood? 
	1. High: [Declare the incident](#COSRunbook-Declaretheincident) and [continue investigation](#COSRunbook-Identifytheproblemandmitigationbasedonthesymptom)
	2. Low: [Continue investigation](#COSRunbook-Identifytheproblemandmitigationbasedonthesymptom)
	3. No: Page secondary COS on-call 
6. Symptom identified? 
	1. Yes: Know a way to mitigate the problem? 
		1. Yes: Problem mitigated 
		2. No: Page secondary COS on-call 
	2. No: Page secondary COS on-call 
7. Problem identified? 
	1. Yes: Know a way to fix the problem?  
		1. Yes: Problem Fixed
		2. No: Page secondary COS on-call 
	2. No: Page secondary COS on-call 
8. Post-analyze the problem 

---

## Impact Analysis 

### Determine the timeline 
1. From the alert triggered, determine the start time of the incident 
2. incident ended, determine the end time too. 
3. identified impact? 
	1. Incident ended: [Continue investigation without declaring incident](#COSRunbook-Identifytheproblemandmitigationbasedonthesymptom)
	2. Incident not ended: [Check for active data center](#COSRunbook-Checkforactivedatacenter)

### Check for active datacenter 
1. Identified impact? 
	1. Inactive datacenter: 
		1. Ask SRE on-call to snooze alerts. 
		2. [Continue investigation without declaring incident](#COSRunbook-Identifytheproblemandmitigationbasedonthesymptom)
	2. Active datacenter: [Perform metric analysis](#COSRunbook-Metricanalysis)

### Metric analysis
1. Analyze the following metrics 
	1. Response time metric i.e. latency [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=43)  
	2. Error rate metric [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=51)
	3. Traffic increase/drop metric
		1. Request rate [Grafana - Overall](https://clovernetwork.grafana.net/d/f626f375-6f8b-44a2-89fc-4588a9292219/platform-health?orgId=1&viewPanel=2),  [Grafana - Success %](https://clovernetwork.grafana.net/d/f626f375-6f8b-44a2-89fc-4588a9292219/platform-health?orgId=1&viewPanel=7) ,  [Grafana - by Service](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=88)
		2. Session rate [Grafana - Overall](https://clovernetwork.grafana.net/d/f626f375-6f8b-44a2-89fc-4588a9292219/platform-health?orgId=1&viewPanel=1) , [Grafana - by Service](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=87)
	4. Availability metric [Grafana - Line chart](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=92) [Grafana - Time series](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=55)
2. Identified impact?
	1. Low: [Continue investigation without declaring incident](#COSRunbook-Identifytheproblemandmitigationbasedonthesymptom)
	2. High: [Check one vs multiple group](#COSRunbook-Onevsmultiplegroups)

### One vs multiple groups
1. Impact groups? 
	1. COSDevice: Device users are impacted -->  High
	2. COSAPI: Webdashboard, Third-party developers, Microservice are impacted  --> High 
	3. COSPayment: Payment non critical traffic are impacted --> High 
	4. SupportServer: ??
	5. COSBatch: Quartz job are impacted --> Low 
	6. COSBoarding: Boarding traffic impacted --> Low 
	7. COSAPK: APK traffic impacted --> Low 
2. Identified impact? 
	1. Low: [Continue investigation without declaring incident](#COSRunbook-Identifytheproblemandmitigationbasedonthesymptom)
	2. High: [Check one vs multiple nodes](#COSRunbook-Onevsmultiplenodes)
### One vs multiple nodes 
1. Check for one or multiple nodes 
	1. Multiple node --> High 
	2. One node --> Low 
2. Identified impact? 
	1. New nodes: Ask SRE on-call to silence the alerts until the node is brought into rotation 
	2. Low: [Continue investigation without declaring incident](#COSRunbook-Identifytheproblemandmitigationbasedonthesymptom)
	3. High: [Declare the incident](#COSRunbook-Declaretheincident)

## Declare the incident 

1. Page Incident on-call manager 
2.  Incident on-call manager 
	1. Create INC JIRA ticket 
	2. Create a public slack channel for engineering team to collaborate and find the root cause 
	3. Create a google meet for mitigation efforts 
	4. COS on-call
3. COS on-call 
	1. Joins the google meet 
	5. Identify the symptom to come up with a mitigation plan 

---

## Identify the problem and mitigation based on the symptom 

### Global load balancer problems
Currently setup only in NA provides TCP level DDoS protection, High availability for HAProxy instances, Single anycast IP with nearest region routing capabilities (and forwarding rule manipulation to target HAProxy servers), TCP-PROXY protocol, that send the session un-altered into our HAProxy balancers, where we inspect the TCP/SSL stream (we need to see TCP native stream).

#### Sudden spike in the request 
1. Understand the symptom and related metrics 
	1. New connection per second metric [Grafana](https://clovernetwork.grafana.net/d/cd860e4e-4d5c-4f10-82a1-be79c88dde2f/gcp-balancer-tcp-proxy?orgId=1&viewPanel=14)
	1. Spike could have been followed by a drop. Drop could have caused by downstream components. When the component recovered, Load balancer could have started processing the retry requests coming from clients. 
2. Probable causes 
	1. [HAProxy sudden drop in request](COS+Runbook#COSRunbook-HAProxysuddendropinrequest)

### HAProxy problems
HAProxy provides Layer 7 load balancing, manipulate the TCP/SSL stream heavily, fingerprinting our device fleet for exceptions and then a large amount of manipulation of HTTP(S) payloads and streams depending on which interface we are using (api/c+d/www/boarding). We also fix device/client issues on the fly as well as protect against various exploits and issues.
#### HAProxy load shedding
1. Understand the symptom and related metrics
	1. HAProxy backend sessions touched the maximum connection (maxconn) limit (NA cosdevice limit: 60K) [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=87)
	2. MaxConn limit helps to stop hundreds of thousands of sessions being send to the COS servers and bogging them down, but rather fail fast and let clients retry without storming herd effect on the application nodes.
	3. Symptom clearly indicates the backend application is degraded in processing capability
	4. Related symptom to watch out for [HAProxy http request queue size increasing](#COSRunbook-HAProxybackendqueuesizeincreasing) 
2. Probable causes 
	1. [High 5xx error](#COSRunbook-COShigh5xxerror)
	2. [Increase in traffic](#COSRunbook-HAProxyIncreaseintraffic)
3. Mitigation effort 
	1. Ensure Maxconn limit is set
4. Short term solution 
5. Long term solution 

#### HAProxy backend queue size increasing 
1. Understand the symptom and related metrics
	1. HAProxy will place the transaction into the backend queue and if it is not serviced, it will generate a `503` and send it back to the client.
	1. HAProxy queue size when the request has not been assigned a backend [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=4)
	1. HAProxy queue time would also have increased. This indicates how long request has not been assigned a backend. [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=90)  
	1. Ideally these should be close to zero to indicate system stability. 
2. Probable causes 
	1. [COS load shedding](#COSRunbook-COSloadshedding)

#### HAProxy sudden drop in request 
1. Understand the symptom and related metrics 
	1. Frontend session count dropped [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=73) 
	1. Total request could would also indicate the slow down [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?viewPanel=panel-88)
2. Probable causes 
	1. [COS load shedding](#COSRunbook-COSloadshedding)
#### HAProxy Increase in traffic
1. Understand the symptom and related metrics
	1. Increase in traffic [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?viewPanel=88)
2. Probable causes 
	1.  Gradual increase in traffic 
		1. Page SRE-on-call 
	1. Spiky increase in traffic 
		1. Could be DDoS ? Slack or Security on-call 
		1. Device retries due to 499 error 
	1. Disaster Recovery cutover? 
		1. Can be ignored as traffic increases when a passive region becomes active 

#### HAProxy marking COS nodes as unavailable 
1. Understand the symptom and related metrics 
	1. How long a give node was marked as down? [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=53)
	2. HAProxy SLB dashboard to see the services which are down [HAProxy dashboard](http://slbdevice01.prod.iad04.clover.network:9876/#billing_live_dc)
		1. Note you need to change to appropriate SLB i.e. slbwww, slbapi and so on. 
2. Probable causes 
	1. [COS nodes out of rotation due to health check failures](#COSRunbook-COShealthcheckfailure)

### Signalscience WAF problems


### COS application problems
Clover operating system (COS) is the monolithic service which provides both metadata information about merchants, developers, resellers, developer apps and so on. Also provides key feature set of products such as orders, non-critical payments, push notification publishing and so on. And also cross cutting concerns such as authentication, capability i.e. authorization, rate-limiting, and so on. 

#### COS errors 
1. Understand the symptom and related metrics
	1. Error dashboard to identify the trending errors [Grafana](https://clovernetwork.grafana.net/d/b7471d51-badd-4a96-8f0a-2e7ef9ad4b12/log-error-trending?orgId=1)
2. Probable causes 
	1. [Database table missing](#COSRunbook-Databasetablemissing) 
	2. [Downstream service or platform not responding](#COSRunbook-Downstreamserviceorplatformnotresponding)
	3. [Database connection error](#COSRunbook-Databaseconnectionnotavailable)
	4. [SQL server running in readonly mode](#COSRunbook-SQLserverrunninginreadonlymode)
3. Mitigation options 
	1. Errors not impacting users 
		1. Impact certain processing, change log level to WARN 
		2. Only for informational purposes, change log level to INFO 
	2. Errors impacting users - Identify the specific root cause 

#### COS node restarted
1. Understand the symptom and related metrics 
2. Probable causes 
3. Mitigation options 
4. Short term fixes 
5. Long term fixes 
#### COS health check failure
1. Understand the symptom and related metrics
	1. COS nodes would be taken out of rotation due to health checks failing in HAProxy. 
	2. HAProxy marking a node as not being available [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=53)
	3. COS health check endpoint might have high latency [Grafana](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=87)
	4. Which nodes are taken out of rotation? [NA device SLB](http://slbdevice01.prod.iad04.clover.network:9876/#client_devices)
2. Probable causes  
	1. Code deployment in-progress
	2. [High memory](#COSRunbook-COShighmemory)
	3. Manually taken out of rotation --> Page SRE-on-call 
	4. Newly added node --> [Silence the alert](#COSRunbook-Silencethealerts)
	5. [Meta primary or order primaries not serving traffic](#COSRunbook-Databaseconnectionnotavailable)
3. Mitigation options 
4. Short term fixes 
5. Long term fixes 

#### COS code deployment issues 
1. Understand the symptom and related metrics
	1. Ensure release is happening 
	2. Ensure the node deployments have completed [Grafana][https://grafana.corp.clover.com/d/xKr00vgVz/na-prod-release-status?orgId=1&search=open&folder=current] 
	3. Continue investigation if the alert did not resolve 
2. Probable causes 
3. Mitigation options 
4. Short term fixes 
5. Long term fixes 

#### COS High CPU 
1. Understand the symptom and related metrics
2. Probable causes 
	1. [HAProxy increase in traffic](#COSRunbook-HAProxyIncreaseintraffic)
	2. [COS high or blocking threads](#COSRunbook-COShighthread)
	4. [COS high memory](#COSRunbook-COShighmemory)
3. Mitigation options 
	1. [Increase CPU](#COSRunbook-IncreaseapplicationCPU)
4. Short term fixes 
5. Long term fixes 

#### COS high network 
1. Understand the symptom and related metrics 
	1. High network bandwidth
		1. TCP traffic received [Grafana](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=253)
		2. TCP traffic sent [Grafana](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=254)
2. Probable causes 
	1. Clients sending huge data in a request <TODO: HAProxy logs to get the in bytes>
	2. Application sending huge data back in response <TODO: HAProxy logs to get the out bytes>
3. Mitigation options 
	1. [Block the handler](#COSRunbook-Blockanhandler) 
4. Short term fixes 
5. Long term fixes 
#### COS high memory 
1. Understand the symptom and related metrics
	1. High JVM memory utilization in percentage [Grafana](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=130)
	2. Manual GC triggered [Grafana](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=99)
		1. Better to disable manual GC trigger as it hides the memory problem and also has not helped a lot in reducing the memory [How?](https://github.corp.clover.com/clover/puppet/pull/9072)
	3. Take a heap dump using rundeck job to identify the problem 
		1. rundeck failure --> Page SRE on call 
2. Probable causes 
	1. Gradual increase over a period of several months 
		1. Discuss with SRE on increasing memory 
	2. Sudden spike or gradual increase after a change 
		1. [Database high number of rows examined](#COSRunbook-Databasehighnumberofrowsreadorwritten)
		2. [COS High network bandwidth](#COSRunbook-COShighnetwork)
		3. [Cos high threads](#COSRunbook-COShighthread)
3. Mitigation options
	1. [Remove manual GC trigger]()
		1. Removing manual GC trigger in the health check endpoint might not mitigate the incident. Though will help identify the root cause. 
	2. [Increase jvm memory](#COSRunbook-Increaseapplicationmemory)
	3. [Add application nodes](#COSRunbook-Addadditionalapplicationnodes)
	4. [Increase the healthcheck endpoint timeout](#COSRunbook-Increasehealthcheckendpointtimeout) 
4. Short term fixes 
5. Long term fixes 

#### COS garbage collection is high 
1. Understand the symptom and related metrics
	1. Not able to find the cause, add the jvmargument to take a heap dump before full GC [Instructions](https://confluence.corp.clover.com/display/ENG/How+to+add+JVM+arguments+to+a+specific+COS+node)
2. Probable causes 
3. Mitigation options 

#### COS high thread 
1. Understand the symptom and related metrics
	1. Take a thread dump using rundeck job  
		1. Thread not revealing anything 
			1. Enable thread dumps
	2. High task executed count for a given executor [Grafana](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=54) 
2. Probable causes
	1. Blocking threads causing an increase in thread dump 
	2. Instantiating thread creation classes in method invocation rather than as a singleton
	3. Making a network call to shared components to fetch/update/delete every resource individually 
3. Mitigation options
	1. [Disable server feature](#COSRunbook-Blockthefeaturebehindtheserverfeatureflag) for non-critical features 
	2. [Puppet config change](#COSRunbook-Puppetconfigchange) to limit thread pool size
	3. [Rolling restart the nodes](#COSRunbook-RestartCOSapplication)
4. Short-term fixes 
	1. Load shed tasks by having a bounded queue 

#### COS threads dying 
1. Understand the symptom and related metrics
	1. Due to exception 
2. Short-term fixes 
	1. Add exception blocks to catch failures that would lead to thread termination 

#### COS High disk 
1. Understand the symptom and related metrics 
2. Probable causes 
	1. High Log writes [Grafana](https://clovernetwork.grafana.net/d/effeea93-35dc-4c51-9fe5-d20b6ceae934/server-status?orgId=1&viewPanel=75)
	2. [High memory](#COSRunbook-COShighmemory)
	3. [High network bandwidth](#COSRunbook-COShighnetwork)
3. Mitigation options
4. Short-term fixes 
5. Long-term fixes 


#### COS drop in 2xx requests 
1. Understand the symptom and related metrics
	1. HAProxy should show the degradation i.e. drop in 2xx [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=88)
	1. Application reporting 2xx count [Grafana]() [Datadog Cosdevice]() [Datadog cosapi]() [Datadog cosbatch]()
2. Probable causes 
	1. [High 5xx error](#COSRunbook-COShigh5xxerror)

#### COS high 5xx error
1. Understand the symptom and related metrics
	1. HAProxy showing high 5xx error [Grafana](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform?orgId=1&viewPanel=86)
	2. Application reporting 5xx error [Grafana](), [Datadog cosdevice](https://app.datadoghq.com/s/21a22b455/pev-fbd-9ft), [Datadog cosapi](), [Datadog cosbatch](), 
2. Probable causes 
	1. [COS load shedding](#COSRunbook-COSloadshedding)
	2. [Node taken out of rotation](#COSRunbook-HAProxymarkingCOSnodesasunavailable)
	3. [Shared resource](#COSRunbook-COSSharedresource)
3. Mitigation options 
	1. 
4. Possible short term fixes 
	1. 
5. Possible long term fixes 

#### COS high 499 error rate
1. Understand the symptom and related metrics 
2. Probable causes 
	1. Increase in traffic ?
		1. Caused due to changing modified time by making bulk updates to tables that are sync-ed to devices  
3. Mitigation options 
	1. [Turn sync off for a merchant](#COSRunbook-Disablesyncrequestforamerchant)

#### COS High latency 
1. Understand the symptom and related metrics 
	1. Response time is high 
	2. 
2. Probable causes 
	1. For a specific endpoint --> Page the team responsible for the handler 
	2. For a specific node 
		1. [Noisy neighbor problem](#COSRunbook-Noisyneighborproblem)
		2. [Config mismatch between nodes](#COSRunbook-COSconfigmismatchbetweennodes)
	3. High request connect time 
3. Mitigation options 


#### COS High connect time 
1. Understand the symptom and related metrics 
	1. HAProxy tracking COS request connect time 
		1. by node [Grafana]()
		2. by service groups [Grafana]()
2. Probable causes
3. Mitigation options 
4. Possible short term fixes 
5. Possible long term fixes 

#### COS load shedding
1. Understand the symptom and related metrics 
2. Probable causes 
	1. [Event executor blocked](#COSRunbook-COSEventexecutorblocked)
	1. [Http executor blocked](#COSRunbook-COSHTTPExecutorblocked)

#### COS Event executor blocked
1. Understand the symptom and related metrics 
2. Probable causes 
	1. Internal downstream service returning 5xx
		1. Page team responsible for 5xx
3. Mitigation options 
4. Short term fixes 
5. Long term fixes 

#### COS HTTP Executor blocked 
1. Understand the symptom and related metrics 
	1. Http thread wait time could be high 
2. Probable causes 
	1. [shared resource problem](COS+Runbook#COSRunbook-COSSharedresource)
	1. [High endpoint latency](#COSRunbook-COSHighlatency)
3. Mitigation options 
	1. [Disable server feature](#COSRunbook-Blockthefeaturebehindtheserverfeatureflag) for non-critical features 

#### COS Tenancy check readability violation 
#### COS Tenancy check writability violation 
#### COS database connections exhausted 
1. Understand the symptom and related metrics 
2. Probable causes 
3. Mitigation options 
	1. [Increase the database connection pool](#COSRunbook-Increaseapplicationdatabaseconnectionpool)

#### COS metric degradation 
1. Understand the symptom and related metrics 
2. Probable causes 
3. Mitigation options 
4. Possible short term fixes 
5. Possible long term fixes 

#### COS config mismatch between nodes 
1. Understand the symptom and related metrics 
2. Probable causes 
3. Mitigation options 
4. Possible short term fixes 
5. Possible long term fixes 

#### COS Shared resource 
1. Probable cause  
	1. [Database](#database)
	1. [Redis](#redis)
	1. [Memcache](#memcache)
	1. [Snowflake]()
	1. [Kafka]()
	1. [Pubsub]()
	1. [Downstream service or platform]()

### Compute Engine problems

#### Node rebooted 
1. Understand the symptom and related metrics
	1. Check in [Google cloud console](https://console.cloud.google.com/logs/query;query=%2528resource.type%3D%22gce_instance%22%2529;duration=PT1H?authuser=1&project=clover-prod-apps)
2. Probable causes 
	1. [New node added and not in use]() --> Ask SRE to mute the alerts 
	2. Maintenance activity 
3. Mitigation options 
4. Short term fixes 
5. Long term fixes 

#### Node added and not in use 
1. Mitigation options 
	1. [Silence the alerts]()

#### Node down 
1. Understand the symptom and related metrics 
	1. Node went down [Cloud monitoring](https://console.cloud.google.com/logs/query;query=resource.type%3D%22gce_instance%22;?project=clover-prod-apps) 
2. Probable causes 
	1. Host failure 
	2. Taken down for maintenance 

#### Noisy neighbor problem 
1. Understand the symptom and related metrics 
2. Probable causes 
3. Mitigation options 
4. Possible short term fixes 
5. Possible long term fixes 
### Database problems

#### Database not available 
1. Slack or page @dbaoncall
2. Understand the symptom and related metrics
	1. Database not available. Uptime metric?
	2. [Database connection not available]()

#### Database connection not available
1. Slack or page @dbaoncall
2. Understand the symptom and related metrics 
	1. COS connection timeout rate [Grafana - Meta primary](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=240) [Grafana - order shards](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=239)
	2. Database Aborted clients metric [Grafana](https://clovernetwork.grafana.net/d/EHD_mpYVk/mysql-server?orgId=1&viewPanel=91)
3. Probable causes 
	1. [Database high disk usage]()
	2. [Database locking issues]()
	3. [Disaster recovery]()
	4. Holding a database connection and calling an external service 
4. Mitigation options 
5. Short term fixes 
6. Long term fixes 

#### Database network issue 
1. Slack or page @networkoncall
2. Understand the symptom and related metrics
	1. 
3. Probable causes 
	1. IP alias missing in the subnet configuration #inc-698
4. Short-term fixes 
5. Long-term fixes 

#### Database high CPU 
1. Slack or page @dbaoncall  
2. Understand the symptom and related metrics 
	1. Database CPU metric [Grafana](https://clovernetwork.grafana.net/d/a7ee3708-2502-4d4d-aaee-5c03c88b4237/mysql-platform?orgId=1&viewPanel=84)
3. Probable causes 
	1. [Database inefficient queries]()
	2. COS making multiple network calls to update each resource individually 
4. Short -term fixes 
5. Long-term fixes 

#### Database high number of threads running 
#### Database locking issues  
1. Slack or page @dbaoncall
2. Understand the symptom and related metrics
	1. High time spent in acquiring locks [Grafana](https://clovernetwork.grafana.net/d/f7261946-fb91-4a98-af24-4b15fe68b812/mysql-instance?orgId=1&viewPanel=171)
	1. Something was holding on to the locks for a long time. 
3. Probable causes 
	1. High Concurrency 
	1. Inefficient Locking Mechanisms
	1. Deadlock 
	1. Long-running transaction 
	1. Inefficient query execution 
4. Short term fixes 
	1. Fine-tune locking configurations such as lock granularity and timeout settings 
	1. Fix inefficient queries 
5. Long term fixes 
	1. Implement transaction batching and caching
#### Database high disk usage
1. Slack or page @dbaoncall
2. Understand the symptom and related metrics
	1. High disk reads regardless of storage engine [Grafana](https://clovernetwork.grafana.net/d/f7261946-fb91-4a98-af24-4b15fe68b812/mysql-instance?orgId=1&viewPanel=219)
	2. High disk reads specific to InnoDB storage engine [Grafana](https://clovernetwork.grafana.net/d/f7261946-fb91-4a98-af24-4b15fe68b812/mysql-instance?orgId=1&viewPanel=146)
3. Probable causes 
	1. Ask DBA on when backups are taken 
	2. [High lock wait time]() could also indicate long-running transactions 
	3. [High number of rows read or written](#high-number-of-rows-examined)

#### Database table missing
1. Slack or page @dbaoncall
2. Understand the symptom and related metrics
	1. 
3. Mitigation options
	1. [Execute DDL statements in database](#execute-ddl-statements-in-database)
	1. [Rollback latest release](#rollback-latest-release)
#### Database inefficient queries 
1. Slack or page @dbaoncall
2. Understand the symptom and related metrics
	1. Clearly indicates that there is a long running transaction which could be timing out
	2. Database server overload 
	3. Lock timeout <TODO: Add a chart for locktimeout metric in MySQL>
3. Probable causes
	1. Database locking issues <TODO: Add a chart for LockTimeOutExeption in COS monitoring>
	2. Full table scan 
	3. Subqueries are bad in MySQL. Joins are better. TODO: Find the source link? 
4. Mitigation options 
	1. [Increase the query timeout value]()
	2. [Kill the long running query]()
	3. [Restart the database server]()
	4. Look at [Database common](#database-common)
5. Short term fixes 
	1. Look at [Database common](#database-common)
	2. Adding index could reduce the number of rows scanned 
	3. [Code fix]() to move the query to database replica if stale reads are ok for few seconds 
	4. Optimize queries
		1. Subquery in insert/update --> replace with join 
		2. Don't select already soft-deleted rows during soft-deletion 
6. Long term fixes 
	1. Refactor using LIKE query because data is stored in TEXT column as json. Better to normalize into their own columns or store in a new table. 
	2. Don't cache data inefficient queries. You are hiding the problem behind cache. 
	3. Look at [Database common](#database-common)

#### Database high number of rows read or written 
1. Slack or page @dbaoncall
2. Understand the symptom and related metrics
	1. Metric to indicate high data reads [Grafana](https://clovernetwork.grafana.net/d/f7261946-fb91-4a98-af24-4b15fe68b812/mysql-instance?orgId=1&viewPanel=146)
		1. Identify which table had maximum reads? [Grafana](https://clovernetwork.grafana.net/d/a64ca396-4c8d-429b-b654-eb0f93010036/mysql-table-statistics?viewPanel=7)
	1. Identify which table had maximum writes? [Grafana](https://clovernetwork.grafana.net/d/a64ca396-4c8d-429b-b654-eb0f93010036/mysql-table-statistics?viewPanel=9)
	1. which handler or job? [Slow query logs]()
3. Probable causes
	1. Read 
		1. Full table scan 
		1. LIKE query 
		1. Scanning not needed rows or columns 
			1. Select ALL
	1. Write 
		1. Changing rows already modified 
			1. Already deleted or updated rows 
4. Mitigation options 
	1. Adding index would reduce the number of rows scanned 
	1. Look at [Database common](#database-common)
5. Short term fixes 
	1. For read query, [Code fix]() to move the query to database replica if stale reads are ok for few seconds 
	1. Batch job needs to reduce the count of rows read or written 
	1. Look at [Database common](#database-common)
6. Long term fixes 
	1. Cache the frequently accessed data  
	1. Look at [Database common](#database-common)

#### SQL server running in readonly mode  
1. Understand the symptom and related metrics
	1. Error message: "java.sql.SQLException: The MySQL server is running with the --read-only option so it cannot execute this statement"
	2. Insert rate near zero [Grafana](https://clovernetwork.grafana.net/d/EHD_mpYVk/mysql-server?orgId=1&viewPanel=114)
	3. Delete rate near zero [Grafana](https://clovernetwork.grafana.net/d/EHD_mpYVk/mysql-server?orgId=1&viewPanel=118)
2. Probable causes 
	1. Active datacenter 
		1. Someone set the primary database to read-only mode. Page DBA on-call 
		2. Database could have crashed and came back in read-only mode. [Database not available]()
		3. Pointing to the wrong database [Puppet]()
	2. Inactive datacenter 
		1. Could be due to devices not flushing DNS and still sending write requests to inactive datacenter. 
3. Mitigation options 
4. Short term fixes 
5. Long term fixes 

#### Database stale data being served 
1. Understand the symptom and related metrics
2. Probable causes 
3. Mitigation options 
4. Short term fixes 
5. Long term fixes 

#### Database common  
1. Mitigation options 
	1. Stop any database or feature migration happening
	1. [Disable the handler in HAProxy]() 
	1. [Pause the batch job]() 
2. Short term fixes 
	1. Reduce the frequency of batch jobs 
	1. Fine-tune the database server config
3. Long term fixes 
	1. Optimize database schema design 
	1. Vertically scale the database node 
	1. Functional decomposition out of COS if the data is not tightly coupled.
	1. Data archiving or purging operation 

### ProxySQL problems


### Redis problems

#### Redis node down 

#### Redis high connection 

#### Redis high CPU 
1. Slack or page @dbaoncall  
2. Understand the symptom and related metrics 
3. Probable causes 
	1. COS making multiple network calls to update each resource individually  
4. Short -term fixes 
5. Long-term fixes 

### Memcache problems
Memcache is used as the application cache and fallbacks to the database when the cache lookup fails. 

#### Memcache node down
1. Understand the symptom and related metrics 
	1. Look at [Node not available]()  
	1. Event executors should not be blocked when memcache node goes down because that would lead to load shedding 

#### Memcache high CPU 
1. Slack or page @dbaoncall  
2. Understand the symptom and related metrics 
3. Probable causes 
	1. COS making multiple network calls to update each resource individually  
4. Short -term fixes 
5. Long-term fixes 
#### Virtual node partially down

#### Memcache not accepting connections 


#### Memcache lookup up methods failed to load 
1. Understand the symptom and related metrics
	1. Application load success count down [Grafana](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=47)
	1. Most of the memcache lookup fallback to database. When this metric is high, it usually means the database did not respond back in time. 
2. Probable causes 
	1. [Database not available]()
	1. [Database connection timeout]() 

### Caffeine cache problems
Few of the caches are stored in COS application memory using caffeine library to avoid network call. 

#### Caffeine cache hit count sudden increase
1. Understand the symptom and related metrics
	1. Application cache hit count metric [Grafana](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=64)
	1. [Http requests increase]()
2. 

### Snowflake problems

### Kafka problems

### Pubsub problems

### Web dashboard problems

### Downstream service or platform problems
1. Understand the symptom and related metrics
	1. Service availability [Grafana](https://clovernetwork.grafana.net/d/ddmb9i781dc74e/haproxy-service-mesh-status?orgId=1&viewPanel=52)
	2. Service returning 5xx [Grafana](https://clovernetwork.grafana.net/d/ddmb9i781dc74e/haproxy-service-mesh-status?orgId=1&viewPanel=51)
	3. Service request rate [Grafana](https://clovernetwork.grafana.net/d/ddmb9i781dc74e/haproxy-service-mesh-status?orgId=1&viewPanel=4)
	4. Service response time [Grafana](https://clovernetwork.grafana.net/d/ddmb9i781dc74e/haproxy-service-mesh-status?orgId=1&viewPanel=43)
	5. Service session rate [Grafana](https://clovernetwork.grafana.net/d/ddmb9i781dc74e/haproxy-service-mesh-status?orgId=1&viewPanel=3)
2. Page team responsible for degradation 
	1. Billing service - Page billing-on-call
	2. Customer service - Page customer-on-call 
3. Probable causes 
4. Mitigation options
	1. [Disable server feature](#block-the-feature-behind-the-server-feature-flag) for non-critical features in the impacted service 
	2. [Puppet change](#fix-the-problem-via-config-change) to reduce time-out 
	3. [Kill blocked threads](#kill-the-threads-in-the-application-layer)
	4. [Rolling restart COS process](#restart-cos-application)
5. Short term fixes 
	1. Circuit breaking in COS 
	2. Moving the request to SlowRequest executor pool to unblock http executor 
	3. Rate-limit in the downstream service 
6. Long term fixes 
	1. Load shedding requests in COS 
	2. Cache requests in COS to avoid multiple calls 
	3. Fallback to a default value instead of retrying 
	4. Async communication with google pub/sub if communication does not need to be synchronous 
	5. Remove COS as a proxy 

---

## How to mitigate the problem 

### Global load balancer mitigation

### HAProxy mitigation

#### Enable maxconn parameter 
1. Restrict HAProxy to limit the number of sessions client can establish.
2. More than that would be temporarily placed in a connection queue 
3. More than what the connection queue can hold is dropped. 
4. Example puppet code: https://github.corp.clover.com/clover/puppet/pull/9070/files 

#### Block an handler 

#### Block IP address in HAProxy

### Signalscience WAF mitigation 

### COS Serverkit application 

#### Block the feature behind the server feature flag 
1. Create an RM ticket 
2. Page release on-call 
3. Create a ticket for the respective team to find the root cause

#### Block the feature behind a setting flag 

#### Disable sync request for a merchant 
1. Cloversports kds do not use clover order sync, but Clover KDS uses clover order sync 
2. 

#### Restart the batch job 
#### Pause the batch job 

#### Disable the third party developer app temporarily

#### Kill the threads in the application layer 
1. 

#### Increase the healthcheck endpoint timeout

#### Increase application jvm memory 
1. Page SRE-on-call 

#### Increase application database connection pool 
1. Page or slack SRE on-call 
2. Create a puppet change to increase the connection pool and ask SRE to review. [Example PR](https://github.corp.clover.com/clover/puppet/pull/4362)
3. Create a CO ticket and ask for approval from leadership team 
4. Restart COS nodes using rundeck once the puppet PR is merged 

#### Disable manual GC 
1. Example: https://github.corp.clover.com/clover/puppet/pull/9072 

#### Restart COS application 
1. Restart via rundeck job 
	1. Rundeck job fails: Page SRE-on-call 


#### Rollback release 



#### Rollback DR 

#### Puppet config change 

#### Rollback puppet change 

#### Rollback terraform change 

### Compute engine 

#### Node not available 
1. Page SRE-on-call
	1. Create an Google priority P1 ticket 
	2. Understand the impact of the node failure on users 

#### Increase application CPU 
1. Page SRE-on-call 

#### Increase application memory 
1. Page SRE-on-call 
2. Example: https://github.corp.clover.com/clover/puppet/pull/9075 

#### Increase application thread pool 
1. Page SRE-on-call  

#### Add additional application nodes  
1. Page SRE-on-call 
2. Example: https://github.corp.clover.com/clover/puppet/pull/9074/
#### Take the affected node out of rotation 

### Network mitigation

#### Disable network access to impacted nodes  
### MySQL Database mitigation



#### Stop the migration 

#### Database query to clean dirty data 

#### Kill slow queries in database 
1. Page DBA-on-call 

#### Add additional replica database nodes 
1. Page DBA-on-call 

#### Restart database nodes 
1. Database nodes 

#### Restore from backup 

### ProxySQL mitigation

### Redis mitigation

### Memcache mitigation

#### Clear memcache 

### Caffeine cache mitigation

#### Clear caffeine cache 

### Snowflake mitigation

### Kafka mitigation

### Pubsub mitigation

### Web dashboard mitigation

#### Block web dashboard requests 

#### Rollback release 

### Downstream service or platform mitigation

### Grafana mitigation

#### Silence the alerts  

### Datadog mitigation

#### Silence the alerts  

--- 


## How to fix the problem 

### Global load balancer fixes 

### HAProxy fixes 

### Signalscience WAF fixes 

### COS Serverkit application fixes 

#### Fix the problem via code change  
1. Create and merge a PR in the master branch 
2. Cherry-pick the change to release branch which was deployed to production if needed for hotfix. 
	1. Page Release team 
	2. Cherry-pick the change to release branch which was cut recently
	3. Release team will merge the release branch PR 
	4. Deploy the change to the staging branch for verification 
	5. Will be eventually deployed to production branch to fix the problem 

#### Fix the problem via config change 
1. Create a puppet PR 
2. Request SRE-on-call to review the change 
3. Merge the PR and perform rolling restarts of COS nodes for the change to reflect. 

### Compute engine fixes 

### Database fixes

#### Execute DDL statements in database 
1. Page DBA-on-call 
2. Ask DBA to execute the statement on the fly to mitigate the incident 
3. Create a PR request in the master branch to add the database script in the server repo 
4. Create a CO ticket to execute the statement in the secondary datacenter 

### ProxySQL fixes

### Redis fixes

### Memcache fixes

### Caffeine cache fixes 

### Snowflake fixes

### Kafka fixes

### Pubsub fixes

### Downstream services fixes

### Web dashboard fixes

### Devices fixes

---


## Post incident work 

1. Follow up tickets are created 
2. 