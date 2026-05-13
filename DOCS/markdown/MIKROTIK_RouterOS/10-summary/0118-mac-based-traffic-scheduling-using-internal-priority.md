## MAC based traffic scheduling using internal Priority 

In Strict Priority scheduling mode, the highest priority queue is served first. The queue number represents the priority and the queue with the highest queue number has the highest priority. Traffic is transmitted from the highest priority queue until the queue is empty, and then moves to the next highest priority queue, and so on. If no congestion is present on the egress port, the packet is transmitted as soon as it is received. If congestion occurs at the port where high-priority traffic keeps coming, the lower-priority queues starve. 

On all CRS switches the scheme where MAC-based egress traffic scheduling is done according to internal Priority would be the following: [MAC address] - > [QoS Group] -> [Priority] -> [Queue]; 

In this example, host1 (E7:16:34:00:00:01) and host2 (E7:16:34:00:00:02) will have higher priority 1 and the rest of the hosts will have lower priority 0 for transmitted traffic on port ether7. Note that CRS has a maximum of 8 queues per port. 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```
