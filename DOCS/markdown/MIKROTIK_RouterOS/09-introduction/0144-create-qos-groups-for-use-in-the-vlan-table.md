## Create QoS groups for use in the VLAN table. 

```
/interface ethernet switch qos-group
add name=group0 priority=0
add name=group1 priority=1
add name=group2 priority=2
```

Add VLAN entries to apply QoS groups for certain VLANs. 

```
/interface ethernet switch vlan
```

```
add ports=ether6,ether7,ether8 qos-group=group0 vlan-id=10
add ports=ether6,ether7,ether8 qos-group=group1 vlan-id=20
add ports=ether6,ether7,ether8 qos-group=group2 vlan-id=30
```

Configure ether6, ether7, and ether8 port queues to work according to Strict Priority and QoS schemes only for VLAN-based QoS. 

```
/interface ethernet switch port
```

```
set ether6 per-queue-scheduling="strict-priority:0,strict-priority:0,strict-priority:0,strict-priority:0,strict-
priority:0,strict-priority:0,strict-priority:0,strict-priority:0" priority-to-queue=0:0,1:1,2:2 qos-scheme-
precedence=vlan-based
```

```
set ether7 per-queue-scheduling="strict-priority:0,strict-priority:0,strict-priority:0,strict-priority:0,strict-
priority:0,strict-priority:0,strict-priority:0,strict-priority:0" priority-to-queue=0:0,1:1,2:2 qos-scheme-
precedence=vlan-based
```

```
set ether8 per-queue-scheduling="strict-priority:0,strict-priority:0,strict-priority:0,strict-priority:0,strict-
priority:0,strict-priority:0,strict-priority:0,strict-priority:0" priority-to-queue=0:0,1:1,2:2 qos-scheme-
precedence=vlan-based
```

Apply bandwidth limit on ether6. 

```
/interface ethernet switch shaper
add port=ether6 rate=10M
```
