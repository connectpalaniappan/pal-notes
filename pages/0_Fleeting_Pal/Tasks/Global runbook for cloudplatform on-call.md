---
tags:
 - nexus/note_log
 - people/pal
 - date/2024-05-09
---
Yesterday:: [[Pal_2024_05_08_Wed]] 
Tomorrow:: [[Pal_2024_05_10_Fri]]  
Today's Journal: [[Pal_2024_05_09_Thu_130th]]

- ## Gcloud
- ## Kubernetes cluster 
  
  | Cluster name                  |     |
  | ----------------------------- | --- |
  | nastaging-us-central1-cluster |     |
- ## Istio ingress gateway
- ## Istio service mesh
- Connectivity check: Make a call from istio service mesh to k8s gateway to COS 
  ```
  NAMESPACE=payment-orchestration-service-dev
  POD=payment-orchestration-service-64f6d458c7-s55sh
  ENDPOINT=http://k8s-gateway.dev.pdx10.clover.network/dev1/cos/api/v3/merchants/C816MB664KY41/orders/Y83Z6FM55YS96/refunds
  kubectl -n $NAMESPACE exec -ti $POD --container istio-proxy -- bash -c 'curl -i --location $ENDPOINT'
  ```
- ## Springboot Application
- ### 401 error code
- Means capability requests are failing
- Either it is a routing problem if it worked in a lower environment
- or capability service is not working when it has affected all the services
- Verify in helm strawberry values the routes are configured correctly
  ```
  externalServices:
    enabled: true
    gateway: 
    rewrite:
  ```
- ### 404 error code
- Routing failed
- Resource does not exist
- ### Header not being passed properly
- Library used for distributed tracing
	- Sleuth integration (Deprecated by brave) https://github.com/openzipkin-attic/sleuth-webmvc-example
	- Brave https://github.com/openzipkin/brave-example
- ## Capability APU
- {appenv="usprod", cloverservice="dataprotection", hostname=~"dataprotection01\\.prod\\.iad01\\.clover\\.network|dataprotection02\\.prod\\.iad01\\.clover\\.network|dataprotection03\\.prod\\.iad01\\.clover\\.network", level="ERROR", log_type="springboot-app"} | json | message=`Failed to invoke capability API`
- ## Pods
- ## Containers
- ## Cloud SQL
- ## Spanner
- ## K8s gateway
- ### K8s gateway node 
  
  | Type                                 | Environment |
  | ------------------------------------ | ----------- |
  | k8s-gateway.dev.dsm09.clover.network | nastaging   |