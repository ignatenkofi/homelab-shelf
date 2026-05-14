## Sub-menu: `/interface bridge mdb` 

**==> picture [502 x 181] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bridge  (name;  The bridge interface to which the MDB entry is going to be assigned.<br>Default: )<br>disabled  (yes | no;  Disables or enables static MDB entry.<br>Default:  no )<br>group  (ipv4 | ipv6 |  The IPv4, IPv6 or MAC multicast address. Static entries for link-local multicast groups 224.0.0.0/24 and ff02::1 cannot be<br>MAC address;  created, as these packets are always flooded on all ports and VLANs.<br>Default: )<br>interface  (name;  The list of bridge ports to which the multicast group will be forwarded.<br>Default: )<br>vid  (integer: 1..4094; The VLAN ID on which the MDB entry will be created, only applies when  vlan-filtering is enabled. When VLAN ID is<br>Default: ) not specified, the entry will work in shared-VLAN mode and dynamically apply on all defined VLAN IDs for particular ports.<br>**----- End of picture text -----**<br>

For example, to create a static MDB entry for multicast group 229.10.10.10 on ports ether2 and ether3 on VLAN 10, use the command below: 

```
/interface bridge mdb
```

```
add bridge=bridge1 group=229.10.10.10 interface=ether2,ether3 vid=10
```

Verify the results with the `print` command: 

```
[admin@MikroTik] > /interface bridge mdb print where group=229.10.10.10
Columns: GROUP, VID, ON-PORTS, BRIDGE
 # GROUP         VID  ON-PORTS  BRIDGE
12 229.10.10.10   10  ether2    bridge1
                      ether3
```

In case a certain IPv6 multicast group does not need to be snooped and it is desired to be flooded on all ports and VLANs, it is possible to create a static MDB entry on all VLANs and ports, including the bridge interface itself. Use the command below to create a static MDB entry for multicast group ff02::2 on all VLANs and ports (modify the `ports` setting for your particular setup): 

369
