## `/interface ethernet switch vlan` 

```
add ports=ether6,ether7,ether8 qos-group=group0 vlan-id=10
add ports=ether6,ether7,ether8 qos-group=group1 vlan-id=20
add ports=ether6,ether7,ether8 qos-group=group2 vlan-id=30
```

Configure ether6, ether7, ether8 port queues to work according to Strict Priority and QoS scheme only for VLAN-based QoS:
