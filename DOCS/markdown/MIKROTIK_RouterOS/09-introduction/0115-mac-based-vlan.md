## MAC Based VLAN 

**==> picture [13 x 13] intentionally omitted <==**

Internally all MAC addresses in MAC-based VLANs are hashed, certain MAC addresses can have the same hash, which will prevent a MAC address from being loaded into the switch chip if the hash matches with a hash from a MAC address that has been already loaded, for this reason, it is recommended to use Port bases VLANs in combination with MAC-based VLANs. This is a hardware limitation. 

**==> picture [504 x 321] intentionally omitted <==**

Switch together the required ports: 

557 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
```

Enable MAC-based VLAN translation on access port: 

```
/interface ethernet switch port
set ether7 allow-fdb-based-vlan-translate=yes
```

Add MAC-to-VLAN mapping entries in the MAC-based VLAN table: 

```
/interface ethernet switch mac-based-vlan
add src-mac=A4:12:6D:77:94:43 new-customer-vid=200
add src-mac=84:37:62:DF:04:20 new-customer-vid=300
add src-mac=E7:16:34:A1:CD:18 new-customer-vid=400
```

Add VLAN200, VLAN300, and VLAN400 tagging on the ether2 port to create it as a VLAN trunk port: 

```
/interface ethernet switch egress-vlan-tag
add tagged-ports=ether2 vlan-id=200
add tagged-ports=ether2 vlan-id=300
add tagged-ports=ether2 vlan-id=400
```

Additionally, add entries to the VLAN table, specify VLAN membership for each port, and enable unknown/invalid VLAN filtering, see an example below - U nknown/Invalid VLAN filtering. This is required for network setups where more interfaces are added to the bridge, as it allows to define VLAN boundaries.
