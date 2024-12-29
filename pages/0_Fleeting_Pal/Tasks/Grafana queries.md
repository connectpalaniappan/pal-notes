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

<mark style="background: #BBFABBA6;">Green color: Need to be added to the dashboard </mark>
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
- <mark style="background: #BBFABBA6;">sum(count_over_time({cloverservice="billing", log_type=~"serverkit-app|cron|secure|serverkit-stdout|messages|secure|haproxy|haproxy-err",hostname=~"bill.+", level!="",level!="INFO"}</mark>
	- https://cloverpos.slack.com/archives/CJHDY1ND9/p1712870352365219?thread_ts=1712237098.744289&cid=CJHDY1ND9
- <mark style="background: #BBFABBA6;">sum(count_over_time({cloverservice="cos::server",level="ERROR"} |="Billing Service Issue" [1m]))</mark>
	- https://cloverpos.slack.com/archives/CJHDY1ND9/p1712870352365219?thread_ts=1712237098.744289&cid=CJHDY1ND9 
- sum(count_over_time( {cloverservice="billing",log_type=~"serverkit-stdout|serverkit-app", appenv="usprod"} !~`java.lang.IllegalStateException` |="duration" | level!="" | json | mdc_handler!="" | line_format "{{.mdc_handler}} {{.message}}" | pattern `<_> duration=<duration> <_>` | duration>2000 | line_format "{{.duration}}" [1m] )) by (level) 
	- https://cloverpos.slack.com/archives/CJHDY1ND9/p1712870352365219?thread_ts=1712237098.744289&cid=CJHDY1ND9 
	- https://clovernetwork.grafana.net/d/edhqv6z1az4lcf/inc-726-bill-web-outage?orgId=1&from=1712228168975&to=1712248899230&var-datasource=b5db12e0-3c48-4cac-9d56-75b69cbdb2c4&viewPanel=3 
- <mark style="background: #BBFABBA6;">Check HATEAOSHandler and LocaleHandler for memcache05 failure</mark> https://clovernetwork.grafana.net/d/NNFA_2JVz/cos-monitoring?orgId=1&var-region=na&var-metric_source=f6ed7c81-31a8-43ae-846e-01d7db12e0c7&var-log_source=b5db12e0-3c48-4cac-9d56-75b69cbdb2c4&var-svc=cos&var-appenv=usprod&var-dc=iad04&var-host_prefix=cosdevice&var-host=All&from=1710952233000&to=1710952842000 
	- Still have a lot of questions to find answer?  
	- Whether the memcache failover happenned ?
	- Still not clear why the 2xx dropped to zero? Just for one memcache node failure? Blocked on event executors 
	- How does memcache perform healthchecks? 
- sum by (mdc_merchantId) (rate({filename="/var/log/cos/cos.log-json",hostname=~"cosdevice.*iad04.*"} | json | mdc_handler="GetOrders" | mdc_httpMethod="GET" | mdc_authMechanism="APP" | mdc_httpStatus="499" |= `No. of values for 'id' exceeded the limit 1000` [$__auto])) 
- sum by (cloverservice) (rate({filename=~"/var/log/haproxy/haproxy.*",hostname=~"slbdevice01.*iad04.*"} != `socket_443` |= ` 499 ` |= `GET` |= `syncId` [$__auto]))

### Application database 
-<mark style="background: #BBFABBA6;"> {appenv="usprod", filename="/var/log/cos/cos.log-json"} |= `meta.primary - Connection is not available` : Meta connection not available: Not added </mark>
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
- <mark style="background: #BBFABBA6;">Bytes increase per endpoint</mark> 


### HAProxy service mesh metric 
- sum(count_over_time( {log_type=~"haproxy",netenv="prod"} | json | __error__ != "JSONParserErr" | haproxy_be_server=~`bill.+` |haproxy_status_code=200 | line_format "{{._entry}}" | pattern `<ipaddr> <ts> <backend> <notsure> <adur1>/<adur2>/<adur3>/<Tber>/<Tdur> <_>` | Tdur>2000 and Tdur<4000 | line_format "{{.__timestamp}} Tber:{{.Tber}} Tdur:{{.Tdur}} status:{{.haproxy_status_code}} server:{{.haproxy_be_server}} entry:{{._entry}}" [1m] )) |="stuck" | json [1m] )) by (mdc_handler)>20 
	- https://cloverpos.slack.com/archives/CJHDY1ND9/p1712870352365219?thread_ts=1712237098.744289&cid=CJHDY1ND9 
- 



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
- <mark style="background: #BBFABBA6;">{hostname=~`cos.+`, level="ERROR"} |="com.clover.dbconnectors.exception.LockTimeoutException" |json | line_format `{{alignRight 10 "LOCKTO:"}} shard={{alignLeft 3 .mdc_shardId_ORDERS}} mid={{alignLeft 8 .mdc_merchantId}} dbmaster={{alignLeft 3 .mdc_dbMasterTime}} totalDtime={{alignLeft 6 .mdc_totalRequestDispatcherTime}} dbmcnt={{alignLeft 6 .mdc_dbMasterCount}} {{.hostname}} {{.mdc_deviceId}} {{.mdc_handler}}`</mark>
	- https://clovernetwork.grafana.net/goto/NVrfHJESR?orgId=1
- The "signature" of the system experiencing what I am thinking is the device nodes getting in each other's way include: 
	- High Row Lock TIME (not waits) <edit>: host_mysql_innodb_lock_row_lock_timed"
	- Lock Timeouts "com.clover.dbconnectors.exception.LockTimeoutException 
	- - High History List Length: host_exec_mysql_innodb_history_list_length 
	- - High read rate on undo logs - Query timeouts "maximum statement time exceeded" 
	- - Long Running Queries on the same merchant_id by distinct cosdevice or cospayment nodes. 
	- - cosdevice and cospayment nodes operating on the same merchant at effectively the same time, give or take sometimes up to a minute or longer cosboarding logging errors that a shard was unavailable. Boarding is trying to lock the merchant_tenancy row for a new merchant, and if it cannot acquire a lock for a merchant_id it throws the error and abandons that id. During the Feb3 event there are large gaps in the usually incrementing mIds
- 

Slow query logs 
- <mark style="background: #BBFABBA6;"> sum(count_over_time( {log_type="mysql-slowlogs"} |="BannerDAO" [1m])) </mark>
	- https://cloverpos.slack.com/archives/CJHDY1ND9/p1712870352365219?thread_ts=1712237098.744289&cid=CJHDY1ND9 
- Slow query logs to get the highest number of rows examined 
	- # Time: 2024-04-01T23:19:57.370269Z # User@Host: metaRW[metaRW] @ [10.137.15.209] Id: 8517349 # Schema: meta Last_errno: 0 Killed: 0 # Query_time: 2098.831414 Lock_time: 0.051886 Rows_sent: 0 Rows_examined: 515871197 Rows_affected: 42465 Bytes_sent: 62
- 

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