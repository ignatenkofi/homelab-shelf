## Per-VLAN offloading 

Since RouterOS 7.21, it is possible to configure L3HW offloading per individual VLAN interface using the `l3-hw-offloading=yes|no` setting in the `/int erface/vlan` menu. This provides finer control over which VLANs (and their related routes) are offloaded to the switch chip, and which are processed by the CPU. It is no longer necessary to disable L3HW on a switch port in order to disable L3HW routing for specific VLANs. 

**==> picture [13 x 13] intentionally omitted <==**

Only VLANs created on a hardware-offloaded, vlan-filtering bridge is capable of L3HW offloading. 

For inter-VLAN routing, both ingress and egress VLANs must have `l3-hw-offloading=yes` , otherwise, the packets are sent to the CPU. 

VLAN interfaces and their related routes now handle the “H” flag independently of switch port configuration. A VLAN ignores the switch port’s L3HW setting and only uses its own. For example, if a VLAN interface has `l3-hw-offloading=yes` , but the switch port for the same VLAN has `l3-hwoffloading=no` , the VLAN interface and its routes will still show the “H” flag, but traffic will be processed by the CPU. 

This design is necessary because multiple VLANs can pass through the same port, and a single VLAN can span multiple ports, where each VLAN and port may have different L3HW settings. 

**==> picture [13 x 13] intentionally omitted <==**

If a switch port carries multiple VLANs with different L3HW settings, keep the port's `l3-hw-enabled=yes` .
