## Enable NAT on the device: 

```
/ip firewall nat
```

```
add action=masquerade chain=srcnat out-interface=ether1
```

Add each port to the VLAN table and allow these ports to access the CPU to make DHCP and routing work: 

```
/interface ethernet switch vlan
```

```
add independent-learning=yes ports=ether2,switch1-cpu switch=switch1 vlan-id=10
add independent-learning=yes ports=ether3,switch1-cpu switch=switch1 vlan-id=20
```

Specify each port to be an access port, and enable secure VLAN mode on each port and on the switch1-cpu port: 

```
/interface ethernet switch port
```

```
set ether2 default-vlan-id=10 vlan-header=always-strip vlan-mode=secure
set ether3 default-vlan-id=20 vlan-header=always-strip vlan-mode=secure
set switch1-cpu vlan-mode=secure
```

**==> picture [13 x 13] intentionally omitted <==**

On QCA8337 and Atheros8327 switch chips, a default `vlan-header=leave-as-is` property should be used. The switch chip will determine which ports are access ports by using the `default-vlan-id` property. The `default-vlan-id` should only be used on access/hybrid ports to specify which VLAN the untagged ingress traffic is assigned to. 

If your device has a switch rule table, then you can limit access between VLANs on a hardware level. As soon as you add an IP address on the VLAN interface you enable inter-VLAN routing, but this can be limited on a hardware level while preserving DHCP Server and other router-related services. To do so, use these ACL rules. With this type of configuration, you can achieve isolated port groups using VLANs. 

```
/interface ethernet switch rule
```

```
add dst-address=192.168.20.0/24 new-dst-ports="" ports=ether2 switch=switch1
add dst-address=192.168.10.0/24 new-dst-ports="" ports=ether3 switch=switch1
```
