## Trunking 

**==> picture [504 x 122] intentionally omitted <==**

The Trunking in the Cloud Router Switches provides static link aggregation groups with hardware automatic failover and load balancing. IEEE802.3ad and IEEE802.1ax compatible Link Aggregation Control Protocol is not supported yet. Up to 8 Trunk groups are supported with up to 8 Trunk member ports per Trunk group. 

Configuration requires a group of switched ports and an entry in the Trunk table: 

```
/interface bridge
add name=bridge1 protocol-mode=none
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```

```
/interface ethernet switch trunk
add name=trunk1 member-ports=ether6,ether7,ether8
```

564 

This example also shows proper bonding configuration in RouterOS on the other end:
