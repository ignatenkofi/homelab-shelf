## Inter-VLAN Routing 

Since L3HW depends on L2HW, and L2HW is the one that does VLAN processing, Inter-VLAN hardware routing requires a hardware bridge underneath. Even if a particular VLAN has only one tagged port member, the latter must be a bridge member. Do not assign a VLAN interface directly on a switch port! Otherwise, L3HW offloading fails and the traffic will get processed by the CPU: 

```
/interface/vlan add interface=ether2 name=vlan20 vlan-id=20
```

Assign the VLAN interface to the bridge instead. This way, VLAN configuration gets offloaded to the hardware, and, with L3HW enabled, the traffic is subject to inter-VLAN hardware routing.
