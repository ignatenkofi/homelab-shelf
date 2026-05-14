## MAC based traffic shaping using internal Priority 

The scheme where MAC based traffic shaping is done according to internal Priority would be following: [MAC address] -> [QoS Group] -> [Priority] -> [Queue] -> [Shaper]; 

In this example, unlimited traffic will have priority 0 and limited traffic will have priority 1 with a bandwidth limit of 10Mbit. Note that CRS has a maximum of 8 queues per port. 

Create a group of ports for switching: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```

Create a QoS group for use in UFDB: 

604 

```
/interface ethernet switch qos-group
add name=group1 priority=1
```

Add UFDB entry to match specific MAC on ether8 and apply QoS group1: 

```
/interface ethernet switch unicast-fdb
```

```
add mac-address=E7:16:34:A1:CD:18 port=ether8 qos-group=group1 svl=yes
```

Configure ether8 port queues to work according to Strict Priority and QoS scheme only for destination address: 

```
/interface ethernet switch port
```

```
set ether8 per-queue-scheduling="strict-priority:0,strict-priority:0,strict-priority:0,strict-priority:0,strict-
prior\
```

```
    ity:0,strict-priority:0,strict-priority:0,strict-priority:0" priority-to-queue=0:0,1:1 \
```

```
    qos-scheme-precedence=da-based
```
