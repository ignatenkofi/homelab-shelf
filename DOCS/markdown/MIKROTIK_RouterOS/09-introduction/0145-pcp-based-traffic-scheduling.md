## PCP-based traffic scheduling 

By default, CRS1xx/CRS2xx series devices will ignore the PCP/CoS/802.1p value and forward packets based on FIFO (First-In-First-Out) manner. When the device's internal queue is not full, then packets are sent in a FIFO manner, but as soon as a queue is filled, then higher-priority traffic can be sent out first. Let us consider a scenario when ether1 and ether2 are forwarding data to ether3 , but when ether3 is congested, then packets are going to be scheduled, we can configure the switch to hold the lowest priority packets until all higher priority packets are sent out, this is a very common scenario for VoIP type setups, where some traffic needs to be prioritized. 

To achieve such a behavior, switch together ether1 , ether2, and ether3 ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether1 hw=yes
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether3 hw=yes
```

Enable Strict Policy for each internal queue on each port: 

570 

```
/interface ethernet switch port
```

```
set ether1,ether2,ether3 per-queue-scheduling="strict-priority:0,strict-priority:0,strict-priority:0,strict-
priority:0,strict-priority:0,strict-priority:0,strict-priority:0,strict-priority:0"
```

Map each PCP value to an internal priority value, for convenience reasons simply map PCP to an internal priority 1-to-1: 

```
/interface ethernet switch port
```

```
set ether1,ether2,ether3 pcp-based-qos-priority-mapping=0:0,1:1,2:2,3:3,4:4,5:5,6:6,7:7
```

Since the switch will empty the largest queue first and you need the highest priority to be served first, then you can assign this internal priority to a queue 1- to-1: 

```
/interface ethernet switch port
```

```
set ether1,ether2,ether3 priority-to-queue=0:0,1:1,2:2,3:3,4:4,5:5,6:6,7:7
```

Finally, set each switch port to schedule packets based on the PCP value: 

```
/interface ethernet switch port
```

```
set ether1,ether2,ether3 qos-scheme-precedence=pcp-based
```
