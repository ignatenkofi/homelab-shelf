## Switch Port Configuration 

Layer 3 Hardware Offloading can be configured for each physical switch port. For example: 

```
/interface/ethernet/switch/port set sfp-sfpplus1 l3-hw-offloading=yes
```

Note that l3hw settings for switch and ports are different: 

433 

Setting `l3-hw-offloading=no` for the switch completely disables offloading - all packets will be routed by CPU. However, setting `l3-hw-offloading=no` for a switch port only disables hardware routing from/to this particular port. Moreover, the port can still participate in Fastrack connection offloading. 

To enable full hardware routing, enable l3hw on all switch ports: 

```
/interface/ethernet/switch set 0 l3-hw-offloading=yes
```

```
/interface/ethernet/switch/port set [find] l3-hw-offloading=yes
```

To make all packets go through the CPU first, and offload only the Fasttrack connections, disable l3hw on all ports but keep it enabled on the switch chip itself: 

```
/interface/ethernet/switch set 0 l3-hw-offloading=yes
```

```
/interface/ethernet/switch/port set [find] l3-hw-offloading=no
```

**==> picture [13 x 13] intentionally omitted <==**

Packets are routed by hardware when both the ingress and egress ports have **`l3-hw-offloading=yes`** . 

If both ingress and egress ports have `l3-hw-offloading=no` , packets will go through the CPU/Firewall while offloading only the Fasttrack connections. 

It is possible to direct packets to go through the CPU/Firewall by setting `l3-hw-offloading=no` on just the egress port. However, setting `l3hw-offloading=no` only the ingress port may cause unpredictable behavior, for example, packets might still be routed by hardware and completely bypass the CPU/firewall. 

The next example enables hardware routing on all ports but the upstream port (sfp-sfpplus16). Packets going to/from sfp-sfpplus16 will enter the CPU and, therefore, subject to Firewall/NAT processing. 

```
/interface/ethernet/switch set 0 l3-hw-offloading=yes
/interface/ethernet/switch/port set [find] l3-hw-offloading=yes
```

```
/interface/ethernet/switch/port set sfp-sfpplus16 l3-hw-offloading=no
```

**==> picture [13 x 13] intentionally omitted <==**

The existing connections may be unaffected by the `l3-hw-offloading` setting change.
