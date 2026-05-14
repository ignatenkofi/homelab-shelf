## Hardware Queues 

Each switch port has eight hardware transmission (tx) queues (queue0..queue7). Each queue corresponds to a traffic class (tc0..tc7) set by a QoS profile. Each ingress packet gets assigned to a QoS profile, which, in turn, determines the traffic class for tx queue selection on the egress port. 

Hardware queues are of variable size - set by the Transmission Manager. Moreover, multiple ports and/or queues can share resources with each other (socalled Shared Buffers). For example, a device with 25 ports has memory (buffers) to queue 1200 packets in total. If we split the resources equally, each port gets 48 exclusive buffers with a maximum of 6 packets per queue (48/8) - which is usually insufficient to absorb even a short burst of traffic. However, choosing to share 50% of the buffers leaves each port with 24 exclusive buffers (3 per queue), but at the same time, a single queue can grow up to 603 buffers (3 exclusive + 600 shared). 

RouterOS allows enabling/disabling the shared pool for each queue individually - for example, to prevent low-priority traffic from consuming the entire hardware memory. In addition, port buffer limits may prevent a single low-speed port from consuming the entire shared pool. See QoS Settings and  Trans mission Manager for details. 

465 

**==> picture [13 x 13] intentionally omitted <==**

The default, best-effort (PCP=0, DSCP=0) traffic class is 1, while the lowest priority (PCP=1) has traffic class 0.
