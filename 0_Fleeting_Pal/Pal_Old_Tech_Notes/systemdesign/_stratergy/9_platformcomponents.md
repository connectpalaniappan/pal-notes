* Responsibilities of platform team
  * Large-scale shared services and developer tools
  * Improve developer experience and productivity

1. [Testing](#testing)
2. [Chaos Engineering](#chaos-engineering)
3. [Authorization/Authentication](#authentication-authorization)
4. [Single Sign On & Identity Management](#identity-management)
5. [Rate-limiting](#rate-limiting)
6. [Static content repository](#storage---content-repository)
7. [API platforms](#api-platforms)
8. [Push Notification](#push-notification)
9. [Email Notification](#email-notification)
10. [Sms Notification](#sms-notification)
11. [Chat-box](#chat-box)

Also includes 
* Collecting application logs, tracing, metrics (Covered in infrastructurecomponents.md)
  * Container orchestration for local development
* Connecting Databases, caches, message queue, scheduler (Covered in corecomponents.md)
* Sharding, api gateway, service mesh, service discovery (Covered in scaleandresiliency.md)
* Communication spec, formats (Covered in tradeoffs.md)

### Testing

#### performance testing
* Load testing
  * Test behavior of a system under a specific expected load
  * Indeed scalable and can handle load we expect
* Stress testing
  * Beyond normal operational capacity often to a breaking point.
  * Identify breaking point in the system i.e. which component will suffer first.
  * What resource it will be: memory, CPU, disk IO.
* Soak testing
  * Test system with typical production load for extended period of time
  * Used to find leaks in system e.g. memory leaks


* Strong auditing system
* Weak auditing system

### Chaos Engineering
* Chaos engineering refers to the practice of intentionally introducing faults into a system in order to test its resilience and ensure applications and engineering teams are able to withstand turbulent and unexpected events. 
* Chaos engineering tool will provide a controlled way to introduce faults and run specific experiments against a particular instance of an application.
* Chaos engineering is embraced by organizations that accept that failures will occur and, instead of trying to prevent failures, practice recovering from them. 
  * This is referred to as optimizing for mean time to repair, or MTTR.
* Software
  * Open Source: Chaos Monkey, Chaos Mesh, Litmus, 
  * Commercial: 
  * AWS: 
  * Azure:
  * GCP:

### Rate limiting

### Authentication Authorization
* Software
  * Open Source: Supertokens ()
  * Commercial: Auth0
  * AWS:
  * Azure:
  * GCP:

### Identity management
* Keycloak is an identity broker which can be used to manage access keys for different services.
* Software
  * Open Source: Spiffe, Spire, Keycloak, Oauth2 Proxy, SSO
  * Commercial: Okta
  * AWS:
  * Azure:
  * GCP:

### Storage - Content repository
* Software
    * Opensource: Wordpress, strapi
    * Commercial: Contentful
    *

### API Platforms
* Software
  * Open Source: Insomnia, Kong, Hoppscotch
  * Commercial: Postman
  * AWS:
  * Azure:
  * GCP:

### Push Notification
* Software
    * Open Source:
    * Commercial: OneSignal,
    * AWS:
    * Azure:
    * GCP:
    * Google: Firebase cloud message
    * Apple: Apple Push Notification service(APNS), Firebase cloud message

### Email Notification
* Software
    * Commercial: Sendgrid, Mailgun, Postmark, SendInBlue
    * AWS: Amazon SES

### Sms Notification
* Software
    * Open source: Asterisk, Wazo
    * Commercial: Twilio
    * AWS:
    * Azure:
    * GCP:

### Chat-box
* Software
    * Open Source: RASA
    * Commercial: Dialogflow
    * AWS:
    * Azure:
    * GCP:
