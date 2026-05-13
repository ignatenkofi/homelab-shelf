## Basic RAW Example 

Let's assume that we have OSPF configuration, but due to connection tracking OSPF have adjacency problems. We can use RAW rules to fix this, by not sending OSPF packets to connection tracking. 

```
/ip firewall raw
add chain=prerouting protocol=ospf action=notrack
add chain=output protocol=ospf action=notrack
```
