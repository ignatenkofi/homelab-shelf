## Create QoS groups for use in the VLAN table: 

```
/interface ethernet switch qos-group
add name=group0 priority=0
add name=group1 priority=1
add name=group2 priority=2
```

Add VLAN entries to apply QoS groups for certain VLANs: 

605
