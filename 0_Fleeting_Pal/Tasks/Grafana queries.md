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


## Common metrics 
- CPU usage 
- Load average 


## Application 
- Endpoint failing 
- Endpoint slow 
- Where time is spent?
- Actually causing errors 

Error per handler, per job 

pattern: "<uri_pattern>" AND reqduration:>10000 

Garbage collection time 
rate(ts("jstat.gc.time", host=web42.prod.clover.com and type=full))

rate(ts(server.handler.*.db.*.db_time.count, source=web42.prod.clover.com)) * ts(server.handler.*.db.*.db_time.mean, source=web42.prod.clover.com) 
## HAProxy metric 
host_haproxy_hrsp_2xx is the number of 2xx requests processed 
host is the slbnodes 


```grafana
sum by (pxname) (rate(host_haproxy_hrsp_2xx{type="frontend", host=~"(<slb nodes>)", pxname!~"(ssl_dispatch|device_.*)"}[$__interval]))
```

5xx error rate 
```
sum by(host, pxname, svname, dc, appenv, puppet_role, serverkit_app, springboot_app) (rate(host_haproxy_hrsp_5xx{appenv=~"usprod|euprod|laprod", type="backend", traffic="slb", pxname!~"serve-404|serve-204|serve-403|ssl_dispatch|device_.*"}[5m]))
```

### TCP connection metric 
```wavefront
rate(ts(net.stat.tcp.failed_accept, env=prod and reason=full_acceptq))
```

HAproxy network bytes 
sum(rate(ts(haproxy.bytes_in, server=web42)))

## Database 

- statistics being outdated on that table and that running the analyze plan might fix this issue https://jira.corp.clover.com/browse/SVR-3864 

Threads running 
```
ts(mysql.threads.running, source=db40-priv.prod.clover.com)
```

```
sum(rate(ts("mysql.threads.created", source=${host})))
```

```
sum(ts(db.shard.0.*.pool.Wait.mean , source=web4*.prod.clover.com), metrics)
```

```
rate(ts(mysql.connections, source=db42-priv.prod.clover.com))
```

Slave delay 
```
ts(db.heartbeat.*.mean, tag=prod-non-api)
```
### Redis 

Memcache 

Node failure https://console.cloud.google.com/logs/query;query=%2528resource.type%3D%22gce_instance%22%0Aresource.labels.instance_id%3D%228280945584517986727%22%0A%2529;cursorTimestamp=2024-03-20T16:37:56.195802Z;startTime=2024-03-18T16:05:55.290Z;endTime=2024-03-24T01:05:55.290Z?project=clover-prod-apps&authuser=0 

### Network
static route may be missing on a router (we don't have BGP yet for this) ... with openvpn to US prod shut down on the rundeck server (as I believe should be the case so that we're not NAT'ing 

### Hardware 
Disk ran out of space 
```
ts("proc.uptime.total", hn=p405) 
```