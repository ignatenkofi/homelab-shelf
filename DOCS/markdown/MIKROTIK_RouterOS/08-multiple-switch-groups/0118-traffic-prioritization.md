## Traffic Prioritization 

The hardware provides two types of traffic transmission prioritization: 

Strict Priority - traffic from higher queues is always transmitted first; 

Enhanced Transmission Selection (ETS) - multiple queues participate in packet transmission scheduling at the same time. 

Strict priority queues are straightforward. If the highest priority queue (Q7) has packets, those are transmitted first. When Q7 is empty, packets from Q6 get transmitted, and so on. The packets from the lowest priority queue (Q0) are transmitted only if all other queues are empty. 

The downside of strict prioritization is increased latency in lower queues while "overprioritizing" higher queues. Suppose the acceptable latency of TC5 is 20ms, TC3 - 50ms. Traffic appearing in Q5 gets immediately transmitted due to the strict priority of the queue, adding extra latency to every packet in the lower queues (Q4..Q0). A packet burst in Q5 (e.g., a start of a voice call) may temporarily "paralyze" Q3, increasing TC3 latencies over the acceptable 50ms (or even causing packet drops due to full queue) while TC5 packets get transmitted at <1ms (way below the 20ms limit). Slightly sacrificing TC5 latency by transmitting TC3 packets in between would make everybody happy. That ETS is for. 

Enhanced Transmission Selection (ETS) schedule traffic for transmission from multiple queues (group members) in a weighted round-robin manner. A queue's weight sets the number of packets transmitted from the queue in each round. For example, if Q2, Q1, and Q0 are the group members, and their weights are 3, 2, and 1, respectively, the scheduler transmits 3 packets from Q2, 2 - from Q1, and 1 - from Q0. The actual Tx order is "Q2, Q1, Q0, Q2, Q1, Q2" - for even fairer scheduling. 

466 

There are two hardware groups: `low-priority-group` and `high-priority-group` . There is a strict priority ordering between the two groups: the lowpriority-group is transmitting only when all queues in the high-priority-group are empty. However, it is possible to use only one group for all queues. 

The default (built-in) RouterOS queue setup is listed below. Q3-Q5 share the bandwidth within the high-priority group, where packets are transmitted while Q6 and Q7 are empty. Q0-Q2 are the members of the low-priority-group, where packets are transmitted while Q3-Q7 are empty. 

```
[admin@MikroTik] /interface/ethernet/switch/qos/tx-manager/queue> print
Columns: TX-MANAGER, TRAFFIC-CLASS, SCHEDULE, WEIGHT, QUEUE-BUFFERS, USE-SHARED-BUFFERS
#  TX-MANAGER  TRAFFIC-CLASS  SCHEDULE             WEIGHT  QUEUE-BUFFERS  USE-SHARED-BUFFERS
0  default     0              low-priority-group   1       auto           no
1  default     1              low-priority-group   2       auto           yes
2  default     2              low-priority-group   3       auto           yes
3  default     3              high-priority-group  3       auto           yes
4  default     4              high-priority-group  4       auto           yes
5  default     5              high-priority-group  5       auto           yes
6  default     6              strict-priority              auto           yes
7  default     7              strict-priority              auto           yes
```

**==> picture [13 x 13] intentionally omitted <==**

It is recommended that all group members are adjacent to each other.
