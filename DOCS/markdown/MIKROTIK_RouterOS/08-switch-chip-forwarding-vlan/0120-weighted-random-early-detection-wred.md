## Weighted Random Early Detection (WRED) 

WRED is a per-queue congestion control mechanism that signals congestion events to the end-points by dropping packets. WRED relies on the existence of rate throttling mechanisms in the end-points that react to packet loss, such as TCP/IP. WRED uses a randomized packet drop algorithm in an attempt to anticipate congestion events and respond to them by throttling traffic rates before the congestion actually happens. The randomness property of WRED prevents throughput collapse related to the global synchronization of TCP flows. 

WRED can be enabled/disabled per each queue in each Tx Manager. Disable WRED for lossless traffic! Also, there is no reason to enable WRED on highspeed ports where congestion should not happen in the first place. 

The behavior is controlled via WRED threshold. WRED threshold is the maximum number of packets/bytes that can exceed the queue shared buffer limit 

(cap). A random packet drop begins when queue usage exceeds their respective capacities: 

`queueX-packet-use > queueX-shared-packet-cap` or 

`queueX-byte-use > queueX-shared-byte-cap` . 

The more usage exceeds capacity, the higher the packet drop chance, reaching 100% at `queueX-shared-packet-cap + wred-packet-threshold` (or byte). 

RouterOS automatically chooses the actual WRED threshold values according to queue or shared pool capacities. The user may shift the thresholds in one way or another via QoS Settings. 

**==> picture [13 x 13] intentionally omitted <==**

WRED requires the respective Tx queues to use shared buffers ( use-shared-buffers=yes ). 

Choosing a WRED threshold value is a tradeoff between congestion anticipation and burst absorption. Setting a higher WRED threshold may lead to earlier traffic rate throttling and, therefore, resolve congestion. On the other hand, a high threshold leads to packet drops in limited traffic bursts that could be absorbed by the queue buffers and transformed losslessly if WRED didn't kick in. For instance, initiating a remote database connection usually starts with heavier traffic ("packet burst") at the initialization phase; then, the traffic rate drops down to a "reasonable" level. Any packet drop during the initialization phase leads to nothing but a slower database connection due to the need for retransmission. Hence, lowering the WRED threshold or entirely disabling WRED on such traffic is advised. The opposite case is video streaming. Early congestion detection helps select a comfortable streaming rate without losing too much bandwidth on retransmission or/and "overshooting" by sacrificing the quality level by too much. 

**==> picture [13 x 13] intentionally omitted <==**

Use Switch Rules (ACL) or other QoS Marking techniques to differentiate traffic and put packets into queues with desired WRED settings. 

The following script only applies WRED to TCP/IP traffic by redirecting it to queue2. UDP and other packets are left in queue1 - since their end-points usually cannot respond to early drops. Queue1 and queue2 are scheduled equally - without prioritizing one queue over another. 

467 

```
/interface/ethernet/switch/qos/profile
```

```
add name=tcp-wred traffic-class=2 pcp=0 dscp=0
```

```
# move TCP traffic to queue2
/interface/ethernet/switch/rule
add new-qos-profile=tcp-wred ports=ether1,ether2,ether3,ether4 protocol=tcp switch=switch1
```

```
# set the same scheduling priority (weight) between queue1 and queue2
```

```
# apply WRED only to queue2 - TCP traffic
```

```
/interface/ethernet/switch/qos/tx-manager/queue/
```

```
set [find where traffic-class=1] weight=2 schedule=low-priority-group use-shared-buffers=yes shared-pool-
index=0 wred=no
```

```
set [find where traffic-class=2] weight=2 schedule=low-priority-group use-shared-buffers=yes shared-pool-
index=0 wred=yes
```
