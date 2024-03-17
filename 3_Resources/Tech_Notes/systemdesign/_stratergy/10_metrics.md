
[Application Metrics](#application-metrics)
[Process metrics](#process-metrics)
[Thread metrics](#thread-metrics)
[Common Database metrics](#common-database-metrics)
[SQL Database metrics](#sql-database-metrics)
[Message queue metrics](#message-queue-metrics)
[Batch/Stream processor metrics](#batchstream-processor-metrics)
[Server Metrics](#virtual-machine-server-metrics)
[Load balancer metrics](#load-balancer-metrics)

### Application metrics
* Application metrics:
  * Alive or not:
* Connection metrics
  * Connection rate: The number of connection attempts (successful or not) to the MySQL server.
  * Open connections: The number of currently open connections.
  * Aborted Clients: The number of connections that were aborted because the client died without closing the connection properly.
  * Aborted Connects: The number of failed attempts to connect.
* Java
  * JVM Heap Usage

### Process metrics
* Process count

### Thread metrics
* Thread count: Total number of threads on the server.
* Thread running: The number of threads that are not sleeping.
* Threads created: The number of threads created to handle connections.
* Threads cached: The number of threads in the thread cache.
* Threadpool Size: Number of threads in the thread pool.
* Idle Threads:
  * Number of inactive threads in the thread pool.
  * Threads become inactive for various reasons, such as by waiting for new work.
  * However, an inactive thread is not necessarily one that has not been assigned work.
  * Threads are also considered inactive if they are being blocked while waiting on disk I/O, or
    * while waiting on a lock, etc.

### Common Database metrics


### SQL Database metrics
* Connection
  * Connection errors accept: The number of errors that occurred during calls to accept() on the listening port.
  * Connection errors max connection: The number of connections refused because the server max_connections limit was reached.
  * Connection errors internal: The number of connections refused due to internal errors in the server, such as failure to start a new thread or an out of memory condition.
  * Connection errors peer address: The number of errors that occurred while searching for connecting client IP addresses.
  * Connection errors select: The number of errors that occurred during calls to select() or poll() on the listening port.
    * (Failure of this operation does not necessarily means a client connection was rejected.)
  * Connection errors tcpwrap: The number of connections refused by the libwrap library.
* Queries
  * Query rate: The number of statements executed by the server.
    * This variable includes statements executed within stored programs.
  * Com Select rate: The Com_select statement counter variables indicate the number of times each select statement has been executed.
  * Com update rate: The Com_update statement counter variables indicate the number of times each update statement has been executed.
  * Com insert rate: The Com_insert statement counter variables indicate the number of times each insert statement has been executed.
  * Com insert select rate: The Com_insert select statement counter variables indicate the number of times each insert select statement has been executed.
  * Com replace rate: The Com_replace statement counter variables indicate the number of times each replace statement has been executed.
  * Com replace select rate: The Com_replace statement counter variables indicate the number of times each replace select statement has been executed.
  * Com delete rate: The Com_delete statement counter variables indicate the number of times each delete statement has been executed.
  * Com begin rate: The Com_insert statement counter variables indicate the number of times each begin statement has been executed.
  * Com commit rate:
  * Com admin rate: Number of admin commands executed. These include table dumps, change users, binary log dumps, shutdowns, pings and debugs.
  * Com delete multi rate:
  * Com update multi rate:
  * Com statement rate: Number of prepared statements prepared.
  * Com statement execute: Number of prepared statements executed.
  * Com statement closed: Number of prepared statements closed (deallocated or dropped).
* Replication
  * Slave io thread running:The status of the I/O thread that transfers the binlogs to the slave. 0 = Not running, 1 = Running.
  * Slave sql thread running: The status of the SQL thread that applies the binlogs to the slave. 0 = Not running, 1 = Running.
  * Seconds behind master: The number of seconds that the slave is behind its master in applying transactions.
* Heartbeat
  * Heartbeat delay status: Percona pt heartbeat delay status
* Durability
  * Xtrabackup runtime: Mysql backup in progress (0 = no, 1 = yes, no data = never did a backup)
  * Handler rollback: The number of requests for a storage engine to perform a rollback operation.
  * Handler savepoint: The number of requests for a storage engine to place a savepoint.

### Message queue metrics
* Publisher ingestion rate

### Batch/Stream processor metrics
* Jobs
  * Active jobs
  * All jobs
* Workers
  * Alive workers
* Stage
  * Waiting stage
  * Running stage

### Network metrics
* Network
  * Network Throughput: Network bytes throughput / second.

### Storage metrics
* Memory
  * Total memory
  * Memory used
  * Memory free
  * Memory utilization
  * Memory active: Memory that has been used more recently and usually not swapped out or reclaimed.
  * Memory inactive: Memory that has not been used recently and can be swapped out or reclaimed
  * Memory Dirty: Memory waiting to be written back to disk.
  * Memory writeBack: Memory which is actively being written back to disk.
  * Memory cached : Memory in the pagecache (Diskcache and Shared Memory).
  * Memory slab : In kernel data structures cache.
  * Memory buffered : Memory in buffer cache, so relatively temporary storage for raw disk blocks. This shouldn't get very large.
  * Memory mapped : Files which have been mmaped, such as libraries,
  * Memory shared : Total used shared memory (shared between several processes, thus including RAM disks, SYS V IPC and BSD like SHMEM)
  * Disk Weighted Service Time: These values count the number of milliseconds that I/O requests have waited on this block device.
    * If there are multiple I/O requests waiting, these values will increase at a rate greater than 1000/second;
    * For example, if 60 read requests wait for an average of 30 ms, the read_time field will increase by 60*30 = 1800
* Disk
  * Bytes data: shows the number of dirty and clean data and index bytes.

### Kubernetes metrics

### Virtual Machine server metrics
* System Load
* Processor (CPUs)
  * Core free
  * Cores used
  * Core utilization
  * Idle utilization
  * IOwait utilization
  * System usage utilization
  * User Core utilization
* Kernel
  * Vmstat pgfault:
    * The page fault handler in the operating system merely needs to make the entry for that page in the memory management unit point to the page in memory and indicate that the page is loaded in memory
    * it does not need to read the page into memory
  * Vmstat pgmajfault:
    * If the page is not loaded in memory at the time of the fault, then it is called a major or hard page fault.
    * The page fault handler in the OS needs to find a free location: either a free page in memory, or a non free page in memory.
    * This latter might be used by another process, in which case the OS needs to write out the data in that page
  * Vmstat pgpgin: Pages paged in by the kernel.
  * Vmstat pgpgout: Pages paged out by the kernel.
  * Vmstat pswpin: Pages swapped in by the kernel.
  * Vmstat pswpout: Pages swapped out by the kernel.
  * Interrupts: An interrupt is an event that changes the sequence of instructions executed by the processor.
  * Entropy Avail : The store of randomness which gets built up by system events (keystrokes, network activity, etc) and drained by the generation of random numbers.
  * Vmstat numa hit: A process wanted to allocate memory from this node, and succeeded.
  * Vmstat numa local: A process ran on this node and got memory from it.
  * Vmstat numa other: A process ran on this node and got memory from another node.
  * vmstat numa miss: A process wanted to allocate memory from another node, but ended up with memory from this node.
  * vmstat numa foreign: A process wanted to allocate on this node, but ended up with memory from another one
* TCP
  * net insegs: Number of TCP segments (TCP chunk + header   no IP encapsulation) received.
  * net outsegs: Number of TCP segments (TCP chunk + header   no IP encapsulation) send.
  * net retranssegs: Number of TCP segments (TCP chunk + header   no IP encapsulation) retransmitted to ensure reliability of TCP segments (due to lost segments for example).
  * nstat TcpExtTCPReqQFullDrop: Increment counter when SYN queue fills up on a socket and we do not send Cookies.
  * nstat TcpExtTCPReqQFullDoCookie: Increment counter when SYN queue fills up on a socket; starting to send Cookies.
  * nstat TcpExtSyncookiesSent: Increment counter when SYN queue fills up and sending a SYN Cookie to remote node.
  * nstat TcpExtSyncookiesRecv: Increment counter when a SYN Cookie was received from a remote node.
  * nstat TcpExtSyncookiesFailed: Increment counter when SYN Cookie was received and the crypto failed, perhaps invalid remote node! 
    * The SYN cookies feature attempts to protect a socket from a SYN flood attack. 
    * This feature is a violation of TCP and conflicts with other areas of TCP such as TCP extensions. 
    * It can cause problems for clients and relays.
  * nstat TcpExtTCPAbortOnData: It means TCP layer has data in flight, but need to close the connection. 
    * So TCP layer sends a RST to the other side, indicate the connection is not closed very graceful. 
    * An easy way to increase this counter is using the SO_LINGER option. 
    * Please refer to the SO_LINGER section of the `socket man page`_: .. _socket man page: http://man7.org/linux/man pages/man7/socket.7.html
    * By default, when an application closes a connection, the close function will return immediately and kernel will try to send the in flight data
    * async. If you use the SO_LINGER option, set l_onoff to 1, and l_linger to a positive number, the close function won't return immediately, but wait for the in flight data are acked by the other side, the max wait time is l_linger seconds. 
    * If set l_onoff to 1 and set l_linger to 0, when the application closes a connection, kernel will send a RST immediately and increase the TcpExtTCPAbortOnData counter.
  * nstat TcpExtTCPAbortFailed: The kernel TCP layer will send RST if the `RFC2525 2.17 section`_ is satisfied. 
    * If an internal error occurs during this process,TcpExtTCPAbortFailed will be increased.
    * nstat TcpExtTCPAbortOnClose: This counter means the application has unread data in the TCP layer when the application wants to close the TCP connection. 
    * In such a situation, kernel will send a RST to the other side of the TCP connection.
    * nstat TcpExtTCPAbortOnLinger: When a TCP connection comes into FIN_WAIT_2 state, instead of waiting for the fin packet from the other side, kernel could send a RST and delete the socket immediately. 
    * This is not the default behavior of Linux kernel TCP stack. 
    * By configuring the TCP_LINGER2 socket option, you could let kernel follow this behavior.
    * nstat TcpExtTCPAbortOnMemory: When an application closes a TCP connection, kernel still need to track the connection, let it complete the TCP disconnect process. 
    * When kernel has not enough memory to keep the orphan socket, kernel would send an RST to the other side, and delete the socket.
    * nstat TcpExtTCPAbortOnTimeout: This counter will increase when any of the TCP timers expire. 
    * In such situation, kernel won't send RST, just give up the connection.
  * nstat TcpExtTCPMemoryPressures: When the amount of memory allocated by TCP exceeds this number of pages, TCP moderates its memory consumption.  
    * This memory pressure state is exited once the number of pages allocated falls below the low mark.
  * TCP Congestion recovery: 
    * When the congestion control comes into Recovery state, if sack is used, TcpExtTCPSackRecovery increases 1, if sack is not used, TcpExtTCPRenoRecovery increases 1. 
    * These two counters mean the TCP stack begins to retransmit the lost packets
  * nstat TcpExtRcvPruned: After 'collapse' and discard packets from the out of order queue, if the actually used memory is still larger than the max allowed memory, this counter will be updated. 
    * It means the 'prune' fails.
  * net attempfails: Number of times that TCP connections made a direct transition to the CLOSED state from either the SYN SENT state or the SYN RCVD state, plus the number of times that TCP connections made a direct transition to the LISTEN state from the SYN RCVD state.
  * net estabresets: The number of times TCP connections have made a direct transition to the CLOSED state from either the ESTABLISHED state or the CLOSE WAIT state.
  * net currestab: The number of TCP connections for which the current state is either ESTABLISHED or CLOSE  WAIT.
  * net activeopens: The rate of TCP active opens (server initiate connection to local or remote port) per second.
  * nstat TcpExtListenOverflows: Increment counter when fully established connections in the Accept Queue fills up, before the application can call accept().
  * nstat TcpExtListenDrops: Increment counter when fully established connections in the Accept Queue fills up, before the application can call accept(), dropping incoming SYN and ACK packets to protect and recover.
  * Netstat close: Local program initiated a close() on the TCP session. No further SENDs will be accepted by the TCP, and it enters the FIN WAIt 1 state.
  * Netstat finwait2: TCP session was placed in FIN1 state (close session was called) and is awaiting an ACK from the connected client. Once ACK is received, the session moves from FIN1 to FIN2.
  * Netstat lastack: TCP session is in closed state (FIN2), but the initiator of the close awaits the final confirmation from the client that the session will be broken down at their end as well.
  * Netstat timewait: After TCP session close, it remains in WAIT state so as to (1) ensure the remote end has closed the connection (for example when LASt ACK is lost) and (2) prevent delayed segments from one connection being accepted by a later connection relying on the same quadruplet.
  * Nstat TcpExtTCPTimeWaitOverflow: When the kernel needs to allocate a new TIME_WAIT socket, the overflow condition is met if the necessary inet_timewait_sock struct is not populated. 
    * This will happen if the current number of TIME_WAIT sockets exceeds tcp_max_tw_buckets OR if allocation of the necessary slab object failed for any reason
  * Netstat closewait: Indicates that the server has received the first FIN signal from the client and the connection is in the process of being closed. 
    * This means the socket is waiting for the application to execute close(). 
    * A socket can be in CLOSE_WAIT state indefinitely until the application closes it.
  * Netstat close: Session state closed.
* UDP
  * net udpoutdatagrams: Number of UDP datagrams send
  * net udpindatagrams: Number of UDP datagrams received
  * net udpinerrors: UDP incoming errors.
  * net udpnoports: UDP no ports.
  * net incsumerrors: UDP incoming checksum errors.

### Load balancer metrics

