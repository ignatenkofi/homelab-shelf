## Simple Queue 

```
/queue simple
```

A simple queue is a plain way how to limit traffic for a particular target. Also, you can use simple queues to build advanced QoS applications. They have useful integrated features: 

peer-to-peer traffic queuing; 

- applying queue rules on chosen time intervals; prioritization; 

- using multiple packet marks from /ip firewall mangle 

- traffic shaping (scheduling) of bidirectional traffic (one limit for the total of upload + download) 

**==> picture [13 x 13] intentionally omitted <==**

Simple queues have a strict order - each packet must go through every queue until it reaches one queue which conditions fit packet parameters or until the end of the queues list is reached. For example, In the case of 1000 queues, a packet for the last queue will need to proceed through 999 queues before it will reach the destination. 

**==> picture [516 x 42] intentionally omitted <==**

696 

Simple queue target matches packets based on src and dst address. If src address matches target, then this is upload, if dst matches target, then this is download. However, if you have a connection where src and dst both match the target, then such packets will always be counted as download since both of them match dst (for each individual packet in both directions) which simply in RouterOS is the first thing compared to the target. Simple queue should be configured in a way that traffic can match only src or dst address, but not both of them at the same time.
