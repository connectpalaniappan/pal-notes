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





## HAProxy metric 
host_haproxy_hrsp_2xx is the number of 2xx requests processed 
host is the slbnodes 


```grafana
sum by (pxname) (rate(host_haproxy_hrsp_2xx{type="frontend", host=~"(<slb nodes>)", pxname!~"(ssl_dispatch|device_.*)"}[$__interval]))
```

### TCP connection metric 
```wavefront
rate(ts(net.stat.tcp.failed_accept, env=prod and reason=full_acceptq))
```

## Monolith metric 



## Database 
