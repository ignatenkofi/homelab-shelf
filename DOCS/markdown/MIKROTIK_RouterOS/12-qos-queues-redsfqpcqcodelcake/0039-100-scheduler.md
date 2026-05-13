## 100% Scheduler 

A queue is 100% Scheduler when there are no packet drops at all, all packets are queued and will be sent out at the first possible moment. 

In each step, the queue must send out queued packets from previous steps first and only then send out packets from this step, this way it is possible to keep the right sequence of packets. 

We will again use the same limit ( 100 packets per step ). 

**==> picture [504 x 221] intentionally omitted <==**

There was no packet loss, but 630 (39,1%) packets had 1 step delay , and the other 170 (10,6%) packets had 2 step delay . (delay = latency)
