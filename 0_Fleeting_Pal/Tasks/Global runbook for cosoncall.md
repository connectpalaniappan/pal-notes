tags:
  - area/pal_employee_monolithobservability
  - date/2024-03-14
priority: P1
assignedTo: people/pal
work: analysis
---

Needs to be documented in [[Incident Management]]
[[Grafana queries]]



--------

[[Cos runbook main document]]


## Resources 
1. COS
	1. [COS monitoring grafana Dashboard](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring)
2. Global TCP Loadbalancer 
	1. [GCP Balancer TCP proxy dashboard](https://clovernetwork.grafana.net/d/cd860e4e-4d5c-4f10-82a1-be79c88dde2f/gcp-balancer-tcp-proxy)
3. HAProxy
	1. [HAProxy grafana dashboard](https://clovernetwork.grafana.net/d/a3fa960a-837a-4440-8b9b-05a44e3af8cc/haproxy-platform)
4. Memcache 
	1. [Memcache grafana dashboard](https://clovernetwork.grafana.net/d/e169d697-a067-4e76-8246-7cc3b5197500/memcached-instance)
5. Redis 
	1. [Redis grafana dashboard](https://clovernetwork.grafana.net/d/d6268005-8e08-4568-99f6-8713fe92312a/redis-instance)
6. ProxySQL 
	1. [ProxySQL grafana dashboard](https://clovernetwork.grafana.net/d/e0a6342b-10f1-4473-82b0-8d174b532690/proxysql-instance)
7. MySQL 
	1. [MySQL grafana dashboard](https://clovernetwork.grafana.net/d/f7261946-fb91-4a98-af24-4b15fe68b812/mysql-instance)
	1. [MySQL table statistics grafana dashboard](https://clovernetwork.grafana.net/d/a64ca396-4c8d-429b-b654-eb0f93010036/mysql-table-statistics)
8. Release 
	1. [Release schedule](https://confluence.corp.clover.com/pages/viewpage.action?pageId=92420453)
9. Disaster Recovery 
10. Rundeck jobs for heap dump, thread dump, restart COS
	1. [Rundeck job](https://rundeck.corp.clover.com/project/self_service/jobs/service_specific)
11. InfraAPI dashboard to query information about nodes 
	1. [InfraAPI dashboard](https://infraapi.global.clover.network/)

--------

monolith-alerts-discussion: "Incase this is an outage, please page cos-oncall-primary.\n Here are useful COS resources:  

--------- 

### Alert investigation

```mermaid
flowchart LR
 Start[Alert Occurred] --> COSonCallTakeCharge[Page Primary Cosoncall]
 subgraph Declare Incident or not 
   COSonCallTakeCharge --> Analysis{Is it Production Issue?}
   Analysis --> |Yes| Impact{Understand the impact} 
   Impact --> |High| Inform[Page Incident on-call]
   CloverImpacted[High users supportcall] --> Declare[Declare Incident]
 end
 subgraph Mitigate Incident  
   Analysis -->|No| IdentifySymptom{Identified the symptom?}
   Impact --> |Low| IdentifySymptom
   Inform --> Declare 
   Declare --> IdentifySymptom
   IdentifySymptom --> |Yes|Mitigate[Mitigate the problem]
   IdentifySymptom --> |No|PageSecondaryCOSonCall[Page Secondary COS on-call]
 end
 subgraph Fix Problem
   Mitigate --> IdentifyProblem{Identified the problem?}
   IdentifyProblem --> |Yes|Fix[Fix the problem]
   IdentifyProblem --> |No|PageSecondaryCOSonCall 
   Fix --> Postanalysis[Post analyze the problem]
 end
```


### Impact analysis 

```mermaid
flowchart LR
  Start[Impact Analysis] --> NodeImpactAnalysis[Check for one or multiple node impact]
  NodeImpactAnalysis --> NodeTypeImpactAnalysis[Check for node type analysis]
  NodeTypeImpactAnalysis --> MetricImpactAnalysis[Check for metric analysis]
```

#### One vs multiple nodes 

```mermaid
flowchart LR
  Start[Impact node analysis] --> CheckMultipleNodes{Check whether it is one or multiple nodes}
  CheckMultipleNodes --> |One node| Low[Low impact]
  CheckMultipleNodes --> |Multiple node|NodeType[Continue to Node Type Analysis]
```

#### One vs multiple type of nodes 


```mermaid
flowchart LR
  Start[Impact nodeType analysis] --> CheckNodeType{Check the type of node}
  CheckNodeType --> |COSDevice| COSDevice[Device users are impacted]
  CheckNodeType --> |COSApi| COSAPI[WebDashboard, Third-party developers and microservice traffic are impacted]
  CheckNodeType --> |COSAPK| COSAPK[APK traffic impacted]
  CheckNodeType --> |COSBoarding| COSBoarding[Boarding traffic impacted] 
  CheckNodeType --> |COSPayment| COSPayment[Payment non-critical traffic impacted]
  CheckNodeType --> |COSBatch| COSBatch[Quartz jobs are impacted] 
  COSBatch --> Low[Low impact]
  COSAPK --> Low 
  COSBoarding --> Low
  COSDevice --> CheckMetricImpact[Check metric impact analysis]
  COSAPI --> CheckMetricImpact 
  COSPayment --> CheckMetricImpact 
```

Metric Analysis



```mermaid
flowchart LR
  Start[Impact metric analysis] --> ImpactMetrics{Analyze Impact Metrics}
  ImpactMetrics --> |Response Time| ResponseTimeMetric{Response Time Metric} 
  ResponseTimeMetric --> AnalyzeImpact{Analyze the impact}
  ImpactMetrics --> |Error Rate| ErrorRateMetric{Error Rate Metric}
  ErrorRateMetric --> AnalyzeImpact
  ImpactMetrics --> |Traffic Drop| TrafficDropMetric{Traffic Drop Metric} 
  TrafficDropMetric --> AnalyzeImpact
  ImpactMetrics --> |Availability| AvailabilityMetric{Availability Metric} 
  AvailabilityMetric --> AnalyzeImpact
  AnalyzeImpact --> |High| HighImpact[High Impact]
  AnalyzeImpact --> |Low| LowImpact[Low Impact]
```
Declare the incident 

```mermaid
flowchart LR
 subgraph COSon-call  
   Mitigator[Cosoncall primary posts on Slack channel #monolith-alerts-discussion] --> PageIncidentOnCall[Page Incident on call manager]
   Mitigator --> CreateMitigatorSlackChannel[COS on-call primary creates a private slack channel to discuss on the symptoms to mitigate]
  end 
  subgraph Incidentmanager-on-call as planner/communicator
    PageIncidentOnCall --> JiraTicket[Incident oncall creates INC JIRA ticket]
    JiraTicket --> CreateCommSlackChannel[Incident oncall creates a public channel for noting down events and communication]
    CreateCommSlackChannel --> CreateGoogleMeet[Incident on-call creates a google meet]
    CreateGoogleMeet --> JoinGoogleMeet[Coson-call primary joins the google meet with other stake holders]
  end

JoinGoogleMeet --> TechnicalFolk{Is the person technical?}
TechnicalFolk --> |Yes| AddMitigatorSlackChannel[Add to private slack channel]
TechnicalFolk --> |No| AddCommSlackChannel[Add to private slack channel]
CreateMitigatorSlackChannel --> TechnicalFolk
```

## Note the timeline 

#### Determine the timeline 

```mermaid
flowchart LR
 Start[Start impact analysis] --> StartTime[Determine the start time of the problem]
 StartTime --> IncidentEnded{Incident ended}
 IncidentEnded --> |Yes|EndTime[Note end time]
```

#### Issue occurred due to an internal change 

```mermaid
flowchart LR
ChangeWindow[Investigate change window] --> 
Deployment{Could be deployment changes?}
Deployment --> PageRelease[Page Release-on-call]
ChangeWindow --> DR{Caused by Disaster recovery changes?}
DR --> PageSRE[Page SRE on-call]
ChangeWindow --> Release{Caused by Release changes?}
Release --> |Yes|PageRelease[Page Release-on-call]
ChangeWindow --> Puppet{Caused by Puppet changes?}
Puppet --> |Yes|PageSRE
ChangeWindow --> Terraform{Caused by terraform changes?}
Terraform --> |Yes|PageNetwork[Page Network-on-call]
```

#### Issue occurred due to external factors 


```mermaid
flowchart LR
 InvestigateExternal[Investigate external changes] --> TrafficIncrease{Was there a traffic increase}
 TrafficIncrease --> |Gradual| GradualIncrease[Did it increase gradually]
 TrafficIncrease --> |Exponential| ExponentialIncrease[Exponential increase in traffic; Could be load problem]
 GradualIncrease --> PageSREonCall[Page SRE-on-call]
 ExponentialIncrease --> PageSecurityOnCall[Page Security on-call; could be DDos]
```





### Identify the problem 

#### Node out of rotation problem 


```mermaid
flowchart LR
 NodeOutOfRotation{Nodes are taken our of rotation?} --> |Yes| ManualGC[Manual GC Triggered] 
 ManualGC --> PageSRE[Page SRE-on-call]
 PageSRE --> DisableManualGC[Disable Manual GC and restart nodes]
 DisableManualGC --> HighMemory{High memory} 

 NodeOutOfRotation --> ServerManuallyTakenOutOfRotation{Is server manually taken out of rotation}
 ServerManuallyTakenOutOfRotation --> PageSREonCall 
 NodeOutOfRotation --> MetaPrimaryHealthCheck[Check on meta primary]
 NodeOutOfRotation --> OrderPrimaryHealthCheck[Check on order primaries]
 
```

#### Load shedding problem 




#### High 5xx error rate



```mermaid
flowchart LR
 5xx{High 5xx error rate} --> LoadShedding[Check for Load shedding]
 LoadShedding --> TODO[TODO]
```


#### High 499 error rate 

```mermaid
flowchart LR
 
```

#### High memory problem 


```mermaid
flowchart LR
 
```


#### High thread problem 

```mermaid
flowchart LR
 
```



#### High disk utilization 

```mermaid
flowchart LR
 
```


#### High error in logs

```mermaid
flowchart LR

```

#### Meta primary database problem 

####  Meta Secondary database problem 

#### Order primary sharded database problem 

#### Order secondary sharded database problem 

#### Memcache problem 

#### Snowflake problem 

#### Kafka problem 

#### Pubsub problem 

#### Webdashboard problem 

#### Downstream service problem 

```mermaid 
flowchart LR 
Start[Start Investigation] --> HighErrorRate[Error rate is high]
HighErrorRate --> 5xx[5xx thrown by a service] 
5xx --> IdentifytheService{Identify the service}
IdentifytheService --> |Customer microservice| CustomerOnCall[Page customer on-call]
```

#### Upstream service problem 

### Collect evidences 
#### High memory evidences 

#### High thread evidences

### Mitigate the problem 

#### Memory mitigation 

```mermaid
flowchart LR
HighMemory[High memory] --> VerticalScale[Add more memory to the node] 
HighMemory --> HorizontallyScale[Add more nodes to increase memory]
```

#### Thread mitigation 




#### Database mitigation 


#### Caffeine Cache mitigation 


#### Memcache mitigation 


#### Snowflake mitigation 


#### Kafka mitigation 


#### Pubsub mitigation 

downstream service mitigation 
#### Upstream service mitigation 

### Root cause analysis 



### Fix the problem 


#### Server feature turn off 

#### Setting turn off 

#### Hotfix deployment 


#### Rollback release 



### Post incident work 





--------

generate a mermaid diagram to identify all the 5xx errors.  Instead of A,B, I need proper names?  Please get deeper into how to investigate these errors in the diagram ?
> [!ai]+ AI Sonnet. Let me stick with it. 
>
> ```mermaid
> graph TD
> Start([Start]) --> IdentifyError[Identify Error Code]
> IdentifyError --> Is500Series{Is it a 5xx Error?}
> Is500Series -- No --> OtherErrors[Handle Other Errors]
> Is500Series -- Yes --> Server500Error[500 Internal Server Error]
> Server500Error --> CheckLogs[Check Application/Server Logs]
> CheckLogs --> IdentifyRootCause[Identify Root Cause]
> IdentifyRootCause --> FixIssue[Fix the Issue]
> FixIssue --> Redeploy[Redeploy Application]
> IdentifyRootCause --> EscalateIfNeeded[Escalate If Needed]
> Is500Series -- Yes --> BadGateway502Error[502 Bad Gateway Error]
> BadGateway502Error --> CheckProxy[Check Proxy/Load Balancer]
> CheckProxy --> RestartServices[Restart Services]
> RestartServices --> VerifyFix[Verify Fix]
> VerifyFix --> FixIssue
> Is500Series -- Yes --> ServiceUnavailable503Error[503 Service Unavailable Error]
> ServiceUnavailable503Error --> CheckCapacity[Check Server Capacity]
> CheckCapacity --> ScaleResources[Scale Resources]
> ScaleResources --> VerifyFix
> Is500Series -- Yes --> GatewayTimeout504Error[504 Gateway Timeout Error]
> GatewayTimeout504Error --> CheckDependencies[Check Downstream Dependencies]
> CheckDependencies --> RestartDependencies[Restart/Fix Dependencies]
> RestartDependencies --> VerifyFix
> Is500Series -- Yes --> HTTPVersionNotSupported505Error[505 HTTP Version Not Supported Error]
> HTTPVersionNotSupported505Error --> CheckConfiguration[Check Server Configuration]
> CheckConfiguration --> UpdateConfiguration[Update Server Configuration]
> UpdateConfiguration --> Redeploy
> FixIssue --> VerifyFix
> VerifyFix
 
> [!ai]+ AI Haiku - need to find the answer by asking multiple times 
>
> ```mermaid
> graph TD
> A(HTTP 500 Internal Server Error) --> B(Investigate server logs for error messages)
> B --> C(Identify the root cause of the error)
> C --> D(Determine the appropriate solution)
> D --> E(Implement the solution and test)
> E --> F(Monitor for recurrence of the issue)
> A(HTTP 500 Internal Server Error) --> G(HTTP 501 Not Implemented)
> G --> H(Ensure the requested functionality is implemented)
> H --> I(Update the server configuration or codebase as needed)
> I --> J(Verify the fix and test thoroughly)
> J --> F(Monitor for recurrence of the issue)
> A(HTTP 500 Internal Server Error) --> K(HTTP 502 Bad Gateway)
> K --> L(Investigate the proxy server or load balancer configuration)
> L --> M(Identify and address any issues with the upstream services)
> M --> N(Ensure the proxy server or load balancer is properly configured)
> N --> F(Monitor for recurrence of the issue)
> A(HTTP 500 Internal Server Error) --> O(HTTP 503 Service Unavailable)
> O --> P(Determine the cause of the service unavailability)
> P --> Q(Scale up resources or optimize the application as needed)
> Q --> R(Ensure the application can handle the expected load)
> R --> F(Monitor for recurrence of the issue)
> A(HTTP 500 Internal Server Error) --> S(HTTP 504 Gateway Timeout)
> S --> T(Investigate the timeout settings for the proxy server or load balancer)
> T --> U(Ensure the upstream services can respond within the configured timeout)
> U --> V(Adjust the timeout settings or optimize the application as needed)
> V --> F(Monitor for recurrence of the issue)
> ```
> The diagram identifies the different 5xx error codes that can occur, and provides a high-level process for resolving them. Here's a breakdown of the steps:
> 1. **HTTP 500 Internal Server Error**:
> - Investigate server logs for error messages to identify the root cause

> [!ai]+ AI Sonnet
>
> ```mermaid
> flowchart LR
> Start([Start]) --> A[Identify the 5xx error]
> A --> B{Is it a 500 Internal Server Error?}
> B -->|Yes| C[Check server logs and application logs for errors]
> C --> D[Identify the root cause and fix the issue]
> B -->|No| E{Is it a 501 Not Implemented Error?}
> E -->|Yes| F[Ensure the requested functionality is implemented]
> F --> D
> E -->|No| G{Is it a 502 Bad Gateway Error?}
> G -->|Yes| H[Check the upstream server or proxy]
> H --> I[Fix the issue with the upstream server or proxy]
> G -->|No| J{Is it a 503 Service Unavailable Error?}
> J -->|Yes| K[Check server load and resources]
> K --> L[Scale resources or implement load balancing]
> J -->|No| M{Is it a 504 Gateway Timeout Error?}
> M -->|Yes| N[Check upstream server response time]
> N --> O[Increase timeout or optimize upstream server]
> M -->|No| P{Is it a 505 HTTP Version Not Supported Error?}
> P -->|Yes| Q[Update server to support the required HTTP version]
> P -->|No| R[Other 5xx error]
> R --> S[Investigate and troubleshoot based on error code]
> D --> End([End])
> I --> End
> L --> End
> O --> End
> Q --> End
> S --> End
> ```
> This Mermaid diagram provides a visual representation of the steps involved in identifying and resolving various 5xx HTTP status codes. It starts by identifying the specific 5xx error code and branches out into different paths based on the error code. Each path provides guidance on troubleshooting and resolving the corresponding error.
> The diagram covers the following error codes:
> - 500 Internal Server Error
> - 501 Not Implemented Error
> - 502 Bad Gateway Error
> - 503 Service Unavailable Error
> - 504 Gateway
 
> [!ai]+ AI Claude 2.1
>
> Unfortunately I do not have enough context to generate a specific mermaid diagram for identifying 5xx errors. As an AI assistant without access to any systems or data, I would need more details about the environment, applications, logs, metrics, etc. to visualize the flow of identifying and troubleshooting errors.
> However, here is an example generic mermaid diagram that could be used as a starting point to visualize the process of handling 5xx errors:
> ```mermaid
> graph TD;
> User-->WebApp;
> WebApp-->200OK;
> WebApp-->5xxError;
> 5xxError-->Logging;
> 5xxError-->Alerting;
> Alerting-->PagerDuty;
> PagerDuty-->OnCallEngineer;
> OnCallEngineer-->Investigate;
> Investigate-->SourceCode;
> Investigate-->Metrics;
> Investigate-->Logs;
> OnCallEngineer-->Mitigate;
> OnCallEngineer-->PostMortem;
> ```
> This shows the high-level flow from a 5xx error being thrown, to logging/alerting, contacting the on-call engineer, investigation steps, mitigation, and follow-up with a post-mortem.
> To make this more specific, I would need more details on the specific systems, applications, error types, logs, metrics collection, alerting tools, etc. But hopefully this gives an idea of how a mermaid diagram can visualize the workflow for handling 5xx errors. Please let me know if you have any other questions!


------


## Key resources

### Establish timelines

1. When release occurred? [Release Schedules, Deployment Timelines & Status](https://confluence.corp.clover.com/pages/viewpage.action?pageId=92420453) 
2. When DR happened? 
    1. Warning: After a DR, you would notice spikes in metric. This is normal. You would need to observe before and after DR to establish whether there was gradual or spikes in the metrics. 

## COS Application

### Memory: High memory utilization > 70% 

1. Verification
    1. Grafana code: (host_jstat_heap_bytes{host=~"cos.*", dc="spl01", heap="old", service="Server"} * 100) / host_jstat_heap_max_bytes{host=~"cos.*", dc="spl01", heap="old", service="Server"}
    2. Grafana metric link: [https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=130&from=1707349143344&to=1707370743344](https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&viewPanel=130&from=1707349143344&to=1707370743344) 
2. Mitigation strategy: [https://confluence.corp.clover.com/display/ENG/%5BRunbook%5D+High+jvm+memory+in+COS+nodes#id-[Runbook]HighjvmmemoryinCOSnodes-RemediationSteps](https://confluence.corp.clover.com/display/ENG/%5BRunbook%5D+High+jvm+memory+in+COS+nodes#id-[Runbook]HighjvmmemoryinCOSnodes-RemediationSteps)

### Key resources

1. Understand node setup in different environment:  
    1. Tutorial on mdb:


```mermaid
flowchart TD
    Start([Alert Received]) --> Analysis{Is it Production Issue?}
    Analysis -->|No| MonitorAndTrack[Monitor and Track]
    Analysis -->|Yes| EvaluateImpact{Evaluate Impact<br/>and Severity}

    EvaluateImpact -->|Minor Impact| MonitorAndTrack
    EvaluateImpact -->|Major Impact| DeclareIncident{Declare Incident<br/>Notify Incident Mgmt Team<br/>Assign Incident Lead<br/>Notify SRE Team}
    DeclareIncident --> NotifySeniorLeaders{Notify Senior Leaders<br/>CTO CEO}
    NotifySeniorLeaders --> CheckServices{Check Services}

    CheckServices --> |Monolith| CheckMonolith{Check Monolith Metrics}
    CheckMonolith --> |High CPU/Mem/Disk| PageMonoTeam[Page Monolith Team]
    CheckMonolith --> |High Errors/Latency| PageMonoTeam
    CheckMonolith --> |Issue in Logs| PageMonoTeam
    PageMonoTeam --> InvestigateMono[Investigate Monolith]
    InvestigateMono --> |SQL| InvestigateSQL[Investigate SQL]
    InvestigateSQL --> |High Connections/Queries| PageSQLTeam[Page SQL Team]
    PageSQLTeam --> FixSQL[Fix SQL Issue]
    FixSQL --> Verify
    InvestigateMono --> |Redis| InvestigateRedis[Investigate Redis]
    InvestigateRedis --> |High Connections/Ops| PageRedisTeam[Page Redis Team]
    PageRedisTeam --> FixRedis[Fix Redis Issue]
    FixRedis --> Verify
    InvestigateMono --> |Memcache| InvestigateMemcache[Investigate Memcache]
    InvestigateMemcache --> |High Misses| PageMemcacheTeam[Page Memcache Team]
    PageMemcacheTeam --> FixMemcache[Fix Memcache Issue]
    FixMemcache --> Verify
    InvestigateMono --> |ExternalService| InvestigateExternal[Investigate External Service]
    InvestigateExternal --> |High Response Time| PageExternalTeam[Page External Service Team]
    PageExternalTeam --> FixExternal[Fix External Service Issue]
    FixExternal --> Verify
    InvestigateMono --> |InternalService| InvestigateInternal[Investigate Internal Service]
    InvestigateInternal --> |High Latency/Errors| PageInternalTeam[Page Internal Service Team]
    PageInternalTeam --> FixInternal[Fix Internal Service Issue]
    FixInternal --> Verify

    CheckServices --> |ExternalService| InvestigateExternal
    CheckServices --> |InternalService| InvestigateInternal

    Verify{Verify Fix}
    Verify -->|Issue Persists| NotifySRE[Notify SRE Team]
    NotifySRE --> CheckServices
    Verify -->|Issue Resolved| Close

    DeclareIncident --> |Monolith Issue| MonoLead[Assign Monolith Team Lead as Incident Lead]
    DeclareIncident --> |SQL Issue| SQLLead[Assign SQL Team Lead as Incident Lead]
    DeclareIncident --> |Redis Issue| RedisLead[Assign Redis Team Lead as Incident Lead]
    DeclareIncident --> |Memcache Issue| MemcacheLead[Assign Memcache Team Lead as Incident Lead]
    DeclareIncident --> |External Service Issue| ExternalLead[Assign External Service Team Lead as Incident Lead]
    DeclareIncident --> |Internal Service Issue| InternalLead[Assign Internal Service Team Lead as Incident Lead]

    DeclareIncident --> IncidentMgmtTeam[Incident Management Team]
    IncidentMgmtTeam --> |Coordination| CoordinateResponse[Coordinate Response]
    CoordinateResponse --> |Communication| CommunicateStatus[Communicate Status]
    CommunicateStatus --> |Documentation| DocumentIncident[Document Incident]
    DocumentIncident --> |Retrospective| ConductRetrospective[Conduct Retrospective]
    ConductRetrospective --> |Improvements| ImplementImprovements[Implement Improvements]

    MonitorAndTrack --> Analysis
    NotifySeniorLeaders --> |Significant Business Impact| InvolveSeniorLeaders[Involve Senior Leaders<br/>CTO, CEO in Response]
    InvolveSeniorLeaders --> CheckServices

    InvolveSeniorLeaders --> CheckServices
```