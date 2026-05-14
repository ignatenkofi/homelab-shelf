## Monitoring and troubleshooting 

This section describes the IGMP/MLD snooping bridge monitoring and troubleshooting options. 

To monitor learned multicast database (MDB) entries, use the `print` command. 

518 

Sub-menu: `/interface bridge mdb` 

**==> picture [454 x 98] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bridge  (read-only: name) Shows the bridge interface the entry belongs to.<br>group  (read-only: ipv4 | ipv6 address) Shows a multicast group address.<br>on-ports  (read-only: name) Shows the bridge ports that are subscribed to the certain multicast group.<br>vid  (read-only: integer) Shows the VLAN ID for the multicast group, only applies when  vlan-filtering  is enabled.<br>**----- End of picture text -----**<br>

```
[admin@MikroTik] /interface bridge mdb print
Flags: D - DYNAMIC
Columns: GROUP, VID, ON-PORTS, BRIDGE
 #   GROUP              VID  ON-PORTS  BRIDGE
 0 D ff02::2              1  bridge1   bridge1
 1 D ff02::6a             1  bridge1   bridge1
 2 D ff02::1:ff00:0       1  bridge1   bridge1
 3 D ff02::1:ff01:6a43    1  bridge1   bridge1
 4 D 229.1.1.1           10  ether2    bridge1
 5 D 229.2.2.2           10  ether3    bridge1
                             ether2
 6 D ff02::2             10  ether5    bridge1
                             ether3
                             ether2
                             ether4
```

To monitor the current status of a bridge interface, use the `monitor` command.
