## In this example: 

Switch port ether6 is using a shaper to limit the traffic that comes from ether7 and ether8. When a link has reached its capacity, the traffic with the highest priority will be sent out first. VLAN10 -> QoS group0 = lowest priority VLAN20 -> QoS group1 = normal priority VLAN30 -> QoS group2 = highest priority 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```
