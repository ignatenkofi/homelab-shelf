## MAC-based traffic scheduling using internal Priority 

In Strict Priority scheduling mode, the highest priority queue is served first. The queue number represents the priority and the queue with the highest queue number has the highest priority. Traffic is transmitted from the highest priority queue until the queue is empty, and then moves to the next highest priority queue, and so on. If no congestion is present at the egress port, a packet is transmitted as soon as it is received. If congestion occurs in the port where high-priority traffic keeps coming, the lower-priority queues starve. 

On all CRS switches the scheme where MAC-based egress traffic scheduling is done according to internal Priority would be the following: [MAC address] - > [QoS Group] -> [Priority] -> [Queue]; In this example, host1 (E7:16:34:00:00:01) and host2 (E7:16:34:00:00:02) will have higher priority 1 and the rest of the hosts will have lower priority 0 for transmitted traffic on port ether7. Note that CRS has a maximum of 8 queues per port. 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```

Create a QoS group for use in UFDB: 

```
/interface ethernet switch qos-group
add name=group1 priority=1
```

Add UFDB entries to match specific MACs on ether7 and apply the QoS group1: 

```
/interface ethernet switch unicast-fdb
add mac-address=E7:16:34:00:00:01 port=ether7 qos-group=group1 svl=yes
add mac-address=E7:16:34:00:00:02 port=ether7 qos-group=group1 svl=yes
```

Configure ether7 port queues to work according to Strict Priority and QoS scheme only for destination address: 

```
/interface ethernet switch port
set ether7 per-queue-scheduling="strict-priority:0,strict-priority:0,strict-priority:0,strict-priority:0,strict-
priority:0,strict-priority:0,strict-priority:0,strict-priority:0" priority-to-queue=0:0,1:1 qos-scheme-
precedence=da-based
```
