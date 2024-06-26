---
tags:
  - project/todo/
  - area/todo/
  - people/todo
  - date/2024-03-25
  - nexus/note_task
priority: P2
assignedTo: people/pal
work: ask
status: Todo
---




## Application 
- Endpoint failing 
- Endpoint slow 
- Where time is spent?
- Actually causing errors 
- Error per handler, per job 
- pattern: "<uri_pattern>" AND reqduration:>10000 
- Garbage collection time : rate(ts("jstat.gc.time", host=web42.prod.clover.com and type=full))
- <mark style="background: #FF5582A6;">Error metric: global.logs.error </mark>
- <mark style="background: #FF5582A6;">Health check endpoint for Clover go: [https://c.clover.com/cos/v1/___ping](https://c.clover.com/cos/v1/___ping) </mark>
- <mark style="background: #FF5582A6;">server.executor.error.request_queued_too_long: Load shedding metric </mark>
- Endpoint for rom updates: /v2/internal/updates. Get's called during device reboots. 

### Application database 
- <mark style="background: #FF5582A6;"> {appenv="usprod", filename="/var/log/cos/cos.log-json"} |= `meta.primary - Connection is not available` : Meta connection not available: Not added </mark>
- host_db_[^shard].*_ConnectionTimeoutRate_m5_rate: Meta connection not available: Added 
- db.shard.0.*.pool.Wait.mean 
- db.heartbeat.*.mean: Slave delay  
- rate(ts(server.handler.*.db.*.db_time.count, source=web42.prod.clover.com)) * ts(server.handler.*.db.*.db_time.mean, source=web42.prod.clover.com) 
- 

#### Application caffeine 
- host_caffeinecache_stats_loadSuccessCount_ 
- host_memcached_.*_hitCount 
## HAProxy metric 
- host_haproxy_hrsp_2xx : 2xx requests processed : added
- host_haproxy_hrsp_5xx: 5xx requests processed: added 
- host_haproxy_qcur: 
- host_haproxy_qtime
- host_haproxy_req_tot: Total request processed 
- host_haproxy_downtime: Downtime of backend service availability 
- haproxy.bytes_in: HAProxy network bytes: 
- net.stat.tcp.failed_accept: TCP connection metric 

## Database 

- mysql.threads.running: Threads running 
- mysql.threads.created: Threads created 
- mysql.connections
- host_mysql_threads_running
- host_diskio_reads: Disk I/O reads 
- host_mysql_innodb_row_lock_time: Row lock time 
- host_mysql_innodb_data_reads: Data reads 
- host_mysql_table_stats_rows_read: Rows read per table 
- host_mysql_table_stats_rows_changed: Rows changed per table 
- host_mysql_table_stats_rows_changed_x_indexes: Rows changed along with indexes 
- host_mysql_schema_table_info_auto_increment: Auto increment row changed 
- statistics being outdated on that table and that running the analyze plan might fix this issue https://jira.corp.clover.com/browse/SVR-3864 
- <mark style="background: #FF5582A6;">telegraf.mysql.handler.read.next: handler read next rate is typically high for databases that have to do a lot of table scans. sequential reads usually a result of table scans.</mark>
- <mark style="background: #FF5582A6;">telegraf.mysql.queries: Number of queries </mark>

ProxySQL 
- <mark style="background: #FF5582A6;">telegraf.exec.proxysql.stats.mysql.connection.pool.queries</mark>

### Redis 

Memcache 

Node failure https://console.cloud.google.com/logs/query;query=%2528resource.type%3D%22gce_instance%22%0Aresource.labels.instance_id%3D%228280945584517986727%22%0A%2529;cursorTimestamp=2024-03-20T16:37:56.195802Z;startTime=2024-03-18T16:05:55.290Z;endTime=2024-03-24T01:05:55.290Z?project=clover-prod-apps&authuser=0 


## Common metrics 
- CPU usage 
- Load average 

### Network
- static route may be missing on a router (we don't have BGP yet for this) ... with openvpn to US prod shut down on the rundeck server (as I believe should be the case so that we're not NAT'ing 

### Hardware 
- proc.uptime.total : Disk ran out of space 


## Root cause analysis 


#### Database conflicts in writes root cause 
- [ ] Unique key constraint violation 
	- [ ] Insert Ignore 
	- [ ] Upsert 