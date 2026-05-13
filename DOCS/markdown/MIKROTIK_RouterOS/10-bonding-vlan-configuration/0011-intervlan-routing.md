## InterVLAN routing 

To create InterVLAN routing, the VLAN interface for each customer VLAN ID must be created on the router and must have an IP address assigned to it. The VLAN interface must be created on the bonding interface created previously. 

Use these commands on the Router : 

```
/interface vlan
add interface=bond_1-2-3-4 name=VLAN10 vlan-id=10
add interface=bond_1-2-3-4 name=VLAN20 vlan-id=20
add interface=bond_1-2-3-4 name=VLAN30 vlan-id=30
/ip address
add address=192.168.10.1/24 interface=VLAN10
add address=192.168.20.1/24 interface=VLAN20
add address=192.168.30.1/24 interface=VLAN30
```

**==> picture [13 x 13] intentionally omitted <==**

These commands are required for DHCP-Server. In case interVLAN routing is not desired but a DHCP-Server on a single router is required, then use Firewall Filter to block access between different subnets. 

**==> picture [13 x 13] intentionally omitted <==**

Since RouterOS v7, it is possible to route traffic using the L3 HW offloading on certain devices. See more details on L3 Hardware Offloading.
