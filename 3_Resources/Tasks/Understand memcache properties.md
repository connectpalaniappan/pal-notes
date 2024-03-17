---
tags:
  - area/employee_cosresiliency
  - people/priya
  - people/brandon
  - date/2024-03-14
priority: P3
assigned to: people/pal
work: analysis
---

EU and LA don't have a separate memcache node 

 min_idle: 40
 max_idle: 54
 test_on_borrow: false
 test_on_return: false
 test_while_idle: true
 tests_per_eviction: 2
 time_between_evictions_ms: 5000
 connection_timeout_ms: 1250
 max_wait: 250
 dead_monitor: true
 dead_span_time: 10000
 dead_span_count: 100
 dead_reset_time: 10000

these are all redis properties 

Note: memcache needs the following  timeout_ms: 2000 

Note memcache instance has the properties 
single_instance: true
port: 11211
memory_mb: 11500
maxconns: 16384
threads: 4
max_reqs_per_event: 100
