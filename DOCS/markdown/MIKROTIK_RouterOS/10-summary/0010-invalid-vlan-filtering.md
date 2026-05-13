## Invalid VLAN filtering 

Since most ports on SwitchA and SwitchC are going to be access ports, you can set all ports to accept only certain types of packets, in this case, we will want SwitchA and SwitchC to only accept untagged packets, use these commands on SwitchA and SwitchC : 

```
/interface bridge port
```

```
set [ find ] frame-types=admit-only-untagged-and-priority-tagged
```

There is an exception for frame types on SwitchA and SwitchC, in this setup access to the management is required from ether1 and bonding interfaces, they require that tagged traffic can be forwarded. Use these commands on SwitchA and SwitchC : 

```
/interface bridge port
```

```
set [find where interface=ether1] frame-types=admit-all
set [find where interface=bond_1-2] frame-types=admit-only-vlan-tagged
```

On SwitchB only tagged packets should be forwarded, use these commands on SwitchB : `/interface bridge port set [ find ] frame-types=admit-only-vlan-tagged` An optional step is to set `frame-types=admit-only-vlan-tagged` on the bridge interface to disable the default untagged VLAN 1 ( `pvid=1` ). We are using the tagged VLAN on the bridge for management access, so there is no need to accept untagged traffic on the bridge. Use these commands on the S witchA , SwitchB and SwitchC : 

```
/interface bridge set [find name=bridge] frame-types=admit-only-vlan-tagged
```

It is required to set up a bridge VLAN table. In this network setup, we need to allow VLAN 10 on ether1-ether8, VLAN 20 on ether9-ether16, VLAN 30 on ether17-ether24, VLAN 10,20,30,99 on bond_1-2, and a special case for ether1 to allow to forward VLAN 99 on SwitchA and SwitchC. Use these commands on SwitchA and SwitchC : 

576 

```
/interface bridge vlan
```

```
add bridge=bridge tagged=bond_1-2 vlan-ids=10
add bridge=bridge tagged=bond_1-2 vlan-ids=20
add bridge=bridge tagged=bond_1-2 vlan-ids=30
add bridge=bridge tagged=bridge,bond_1-2,ether1 vlan-ids=99
```

**==> picture [13 x 12] intentionally omitted <==**

Bridge ports with `frame-types` set to `admit-all` or `admit-only-untagged-and-priority-tagged` will be automatically added as untagged ports for the `pvid` VLAN. 

Similarly, it is required to set up a bridge VLAN table for SwitchB. Use these commands on SwitchB : 

```
/interface bridge vlan
add bridge=bridge tagged=bond_1-2,bond_3-4,bond_5-6-7-8 vlan-ids=10,20,30
add bridge=bridge tagged=bond_1-2,bond_3-4,bond_5-6-7-8,bridge vlan-ids=99
```

When everything is configured, VLAN filtering can be enabled. Use these commands on SwitchA , SwitchB, and SwitchC : 

```
/interface bridge
set bridge vlan-filtering=yes
```

**==> picture [13 x 13] intentionally omitted <==**

Double-check if port-based VLANs are set up properly. If a mistake was made, you might lose access to the switch and it can only be regained by resetting the configuration or by using the serial console. 

**==> picture [13 x 12] intentionally omitted <==**

VLAN filtering is described more in the Bridge VLAN Filtering section.
