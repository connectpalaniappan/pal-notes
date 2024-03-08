### API Principles
1) REST (Representational state transfer of resources)
2) Best practice of HTTP API to interact with resources.
3) URL only decides the location.
4) Headers (Accept and Content-Type, etc.) decide the representation.
5) HTTP methods(GET/POST/PUT/DELETE) decide the state transfer.
   1) POST body is more secure and encrypted.
6) Minimize the coupling between client and server (a huge number of HTTP infras on various clients, data-marshalling).
7) stateless and scaling out. 
8) service partitioning feasible. 
9) used for public API.
10) URI must be nouns, not verbs
    /cars
    /users
    /books/{id}
11) Don't use hierarchial pattern in the data model
12) Version your API
    Path: /v1/users
    Subdomain: api.v1.example.com/users
13) All nouns are plurals
    GET /users
    DELETE /users/{id}
    GET /users/{id}/reviews
    POST /users/{id}/reviews
    PUT /users/{id}/reviews/{reviewid}
14) Map relations by sub-resources
    GET /users/{id}/reviews
    PUT /users/{id}/reviews/{reviewid}
15) Allow for collections filtering, sorting and paging
    GET /users/{id}/reviews?published=1
    GET /users?sort[]=-age&sort[]=+name
    GET /books?format[]=epub&format[]=mobi
    GET requests must never alter system/resource state (GET is readonly)
16) Identify all the resources 
    1) Few resources are atomic; most are collections or views of other resources 
    2) Do not confuse identity (naming) with containment (storage)
    3) Resources have more in common with procedures than they do with records or files 
17) Iteratively develop resources and uses cases (state transitions)
    Do not try to do everything at once
    Do not make any assumption about received content, order, versioning, etc. 
18) APIs are Forever
19) Never Break Backward Compatibility
20) Work Backwards from Customer Use Cases
21) Create APIs That are Self Describing and Have a Clear, Specific Purpose
22) Create APIs with Explicit and Well-Documented Failure Modes
23) Avoid Leaking Implementation Details at All Costs

HATEAOS
HTTP Methods
Content Negotiation
Character Encoding
Pagination
path param
query
