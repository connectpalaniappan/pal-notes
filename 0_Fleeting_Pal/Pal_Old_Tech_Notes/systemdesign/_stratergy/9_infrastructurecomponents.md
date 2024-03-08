*Responsibilities owned by infrastructure team (includes Devops, security and network team)
  * Setting up the cluster, provisioning instances
  * Continuous integration and deployment
  * Helping application engineers write infrastructure as a code

1. [System Observability - Logging](#system-observability---logging)
2. [System Observability - Monitoring](#system-observability---monitoring)
3. [System Observability - Tracing](#system-observability---tracing)
4. [Continuous integration](#continuous-integration)
5. [Continuous deployment](#continuous-deployment)
6. [Image Definition](#container-image-definition)
7. [Image Build](#container-image-build)
8. [Image registry](#container-image-registry)
9. [Container runtime](#container-runtime)
10. [Container orchestration](#container-orchestration)
11. [Configuration service](#configuration-service)
12. [Automation service](#automation-service)
13. [Infrastructure provisioning](#infrastructure-provisioning)
14. [Cloud native network](#cloud-native-network)
15. [Security compliance](#security-and-compliance)
16. [Secret manager](#secret-key-management)

### System Observability - Logging
* Applications emit a steady stream of log messages describing what they are doing at any given time. 
* These log messages capture various events happening in the system such as failed or successful actions, audit information, or health events. 
* Logging tools collect, store, and analyze these messages to track error reports and related data.
* log collection tools like Fluentd run alongside application containers and collect messages directly from the applications. 
  * Messages are then forwarded on to a central log store to be aggregated and analyzed.
* Software
  * Open Source: Fluentd, Elasticsearch, Logstash and Kibana (ELK), Opensearch, Grafana Loki,
  * Commercial: Splunk, Sumologic
  * AWS: AWS Cloudwatch
  * Azure:
  * GCP:

### System Observability - Monitoring
* Monitoring refers to instrumenting an app to collect, aggregate, and analyze logs and metrics to improve our understanding of its behavior.
* Define SLO, SLI and SLA goals.
* Monitor the performance of the service?
* Alerts when critical components fail?
* Includes both metrics and tracing
* Software
  * Open Source: Prometheus, Cortex, Openmetrics, Thanos, Skywalking, Signoz, Graphite
  * Commercial: Appdynamics, datadog, New relic, dynatrace, wavefront
  * AWS:
  * Azure:
  * GCP: Google stackdriver

### System Observability - tracing
* In a microservices world, services are constantly communicating with each other over the network. 
* Tracing, a specialized use of logging, allows you to trace the path of a request as it moves through a distributed system.
* Tracing solves this problem by adding a unique identifier to messages sent by the application. 
  * That unique identifier allows you to follow (or trace) individual transactions as they move through your system.
* Software
  * Open Source: Jaeger, OpenTelemetry, OpenTracing, Zipkin, Spring cloud sleuth
  * Commercial: 
  * AWS: 
  * Azure:
  * GCP:
  
### Continuous integration
* CI automates code changes by immediately building and testing the code, ensuring it produces a deployable artifact.
* CI system sees the code change, then builds and tests a new version of an app.
* Software
  * Open Source: Jenkins, Argo, Flux, Teamcity, Travis CI, Github actions
  * Commercial: 
  * AWS: 
  * Azure:
  * GCP:

### Continuous deployment
* CD pushes the artifact through the deployment phases.
* CD system takes that new version and deploys it into a dev, test, pre-production, and finally production environment.
* Software
  * Open Source: Spinnaker, Helm
  * Commercial: Harness
  * AWS: AWS Codedeploy
  * Azure:
  * GCP:

### Container Image definition
* Developer-focused tools that help build application code into containers and/or Kubernetes
* How to correctly write, package, test, or run custom apps.
* Software
  * Open Source: Docker File, Docker Compose
  * Commercial:
  * AWS:
  * Azure:
  * GCP:

### Container Image Build
* Operations-focused tools that deploy apps in a standardized way.
* Deploying and managing applications.
* Helm is flexible enough to allow users to customize their own app deployments and is often used by organizations for their own internal releases.
* Software
  * Open Source: Helm, Docker compose, Skaffold, Podman, JKube (SaaS), Shipwright (SaaS)
  * Commercial: 
  * AWS:
  * Azure:
  * GCP:

### Container Image registry
* Definition
  * Container is "a running process with resource and capability constraints managed by a computer’s operating system".
  * Image is a set of archive files needed to run containers and its process. You could see it as a form of template on which you can create an unlimited number of containers.
  * Repository, or just repo, is a space to store images.
* Container registries either store and distribute images or enhance an existing registry in some way. 
* Fundamentally, a registry is a web API that allows container runtimes to store and retrieve images.
* Many provide interfaces to allow container scanning or signing tools to enhance the security of the images they store. 
* Some specialize in distributing or duplicating images in a particularly efficient manner.
* Software
  * Open Source: Harbor, Dragonfly, 
  * Commercial: JFrog artifactory
  * AWS: Elastic Container Registry
  * Azure: Azure Registry
  * GCP: Google container registry
  * IBM: IBM Cloud container registry

### Container runtime
* Container runtime is the software that executes containerized (or "constrained") applications.
* Launches apps in a standardized fashion across all environments and sets security boundaries.
* Software
    * Open Source: Container-d, cri-o, rkt(archived), kata
    * Commercial: 
    * AWS:
    * Azure:
    * GCP:

### Container orchestration
* Orchestration and scheduling refer to running and managing containers across a cluster. 
* A cluster is a group of machines, physical or virtual, connected over a network (see cloud native networking).
* Kubernetes does something called desired state reconciliation: 
  * it matches the current state of containers within a cluster to the desired state. 
  * The desired state is specified by the engineer
* If the desired and actual state don't match, Kubernetes reconciles them by creating or destroying objects.
* Software
    * Open Source: Kubernetes, Docker swarm, Hashicorp, Mesos, Crossplane, Nomad, Fluid, Volcano
    * Commercial:
    * AWS: Amazon ECS
    * Azure: Azure Kubernetes Engine
    * GCP: Google Kubernetes Engine

### Configuration service
* Configuration tools speed up configuration of compute resources (virtual machines, networks, firewall rules, load balancers, etc.)
* Software
  * Open Source: Puppet, Chef, Ansible, Saltstack,
  * Commercial:
  * AWS:
  * Azure:
  * GCP:

### Automation service
* Software
  * Open Source: Rundeck,
  * Commercial:
  * AWS:
  * Azure:
  * GCP:

### Infrastructure provisioning
* Automation speed up the creation of compute resources (virtual machines, networks, firewall rules, load balancers, etc.).
* Automated tools like Terraform reduce the level of effort required to scale tens of servers and networks with hundreds of firewall rules.
* Software
  * Open Source: Pulumi, Terraform
  * Commercial:
  * AWS: AWS Cloudformation
  * Azure:
  * GCP:

### Cloud native network
* Containers talk to each other and to the infrastructure layer through a cloud native network.
* Distributed applications have multiple components that use the network for different purposes.
* Tools create a virtual network on top of existing networks specifically for apps to communicate, referred to as an overlay network.
* Products use Container Network Interface (CNI), a CNCF project, to provide networking functionalities to containerized applications.
* Software
  * Open Source: Cilium, CNI, Antrea, Flannel, Network service mesh, Calico
  * Commercial:
  * AWS:
  * Azure:
  * GCP:

### Security and compliance
* Responsibilities
  * Image scanning
  * Image signing
  * Policy creation and enforcement
  * Audit
  * Certificate Management
  * Network layer security
* Software
    * Open Source: Open Policy Agent, Tuf, Falco, Notary, Terrascan
    * Commercial: checkmarx, Synk, Fairwind Insights, Nexus repository
    * AWS:
    * Azure:
    * GCP: 

### Secret key management
* Key generation, storage, management, and rotation
* Vault is a rather generic key management tool allowing you to manage different types of keys
* Software
  * Open Source: Vault 
  * Commercial:
  * AWS:
  * Azure:
  * GCP: Google secret manager, Google KMS
