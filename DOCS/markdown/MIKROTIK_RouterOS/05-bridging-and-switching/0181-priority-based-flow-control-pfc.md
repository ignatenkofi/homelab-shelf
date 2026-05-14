## Priority-based Flow Control (PFC) 

Priority-Based Flow Control (PFC) provides lossless operation for up to eight traffic classes, so that congestion in one traffic class does not pause other traffic classes. In addition, PFC enables co-existence of loss-sensitive traffic types with loss tolerant traffic type in the same network. 

PFC-capable switch chips are complaint with IEEE 802.1Qbb PFC, meaning that the respective devices are capable of generating and responding to PFC frames. On the triggering part, the PFC frame is sent by the source port and traffic class experiencing the congestion. The timer values of the generated PFC frames are 0xFFFF for pause (XOFF) and 0x0 for resume (XON), and the appropriate bit in the priority enable vector is set. On the response part, the received PFC frame pauses the specific priority queues on the port that received the PFC frame for the duration specified by the PFC frame. 

In RouterOS, PFC configuration is organized in profiles, where each port can be assigned to a specific profile. A PFC profile defines the traffic classes to enable PFC on, pause/resume thresholds to send XOFF/XON PFC frames, respectively, and whenever the assigned ports should transmit or/and receive PFC frames. 

While congestion occurs on egress ports, PFC is triggered on the ingress port. Shared buffers must be used to associate the amount of ingressed traffic with the respective packets waiting in Tx queues. For each PFC-enabled traffic class, set use-shared-buffers=yes to the respective Tx Queues. It is also recommended that a separate shared pool ( shared-pool-index ) be used for each PFC-enabled queue, especially not to mix it with PFC-disabled traffic classes. 

**==> picture [13 x 13] intentionally omitted <==**

RouterOS implements 1:1 mapping between traffic classes and Tx queues. Packets with assigned traffic class 0 get enqueued in queue0, TC1 - queue1, etc., up to TC7-Q7. Hence, the terms "traffic class" and "tx queue" are used interchangeably in this text. 

468 

When choosing pause and resume thresholds, consider a delay in transmitting a PFC frame and processing it by the other side. For example, device A experienced congestion at time T, transmitted a PFC pause frame to device B, and B processed the frame and halted transmission at time T+D. During the delta time D, device B still kept sending traffic. If device A has configured the pause threshold to 100%, it has no free buffers available, and, therefore, packets may drop, which is unacceptable for lossless traffic classes. Lowering the pause threshold, let's say, down to 80% issues a PFC pause frame while still having free memory to accumulate traffic during the delta time D. The same applies to resume threshold. Setting it to 0% keeps the device idle during the delta time, lowering the overall throughput. 

PFC Rx requires setting the egress rate to all associated queues to calculate pause time, even if it matches the wire speed. For example, if PFC runs on traffic class 3, the assigned ports require the `egress-rate-queue3` setting. 

```
/interface/ethernet/switch/qos/priority-flow-control add name=pfctc3 traffic-class=3 rx=yes
/interface/ethernet/switch/qos/port set sfp-sfpplus1,sfp-sfpplus2 pfc=pfctc3 egress-rate-queue3=10G
```
