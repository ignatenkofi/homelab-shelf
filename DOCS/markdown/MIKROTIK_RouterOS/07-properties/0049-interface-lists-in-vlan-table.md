## Interface lists in VLAN table 

Starting from RouterOS version 7.17, you can use interface lists for the `tagged` and `untagged` properties in the bridge VLAN table. This change allows for more flexible VLAN assignment to ports by simply modifying the interface list members, rather than updating each bridge VLAN entry individually. 

If different interface lists are specified for the `tagged` and `untagged` settings, and there is overlap between the interface members, the `untagged` list will take priority. You can check the current interface configuration with `current-tagged` and `current-untagged` properties using the `print` command. 

Below is an example where new interfaces are added to already existing interface lists. This shows how the bridge port and VLAN tables are automatically updated without directly changing settings in those menus. 

```
/interface list
add name=vlan10_untagged
add name=vlan20_untagged
add name=vlan_tagged
/interface list member
add interface=ether2 list=vlan10_untagged
add interface=ether3 list=vlan10_untagged
```

363 

```
add interface=ether4 list=vlan20_untagged
add interface=sfp-sfpplus1 list=vlan_tagged
/interface bridge
add frame-types=admit-only-vlan-tagged name=bridge1 vlan-filtering=yes
/interface bridge port
add bridge=bridge1 frame-types=admit-only-untagged-and-priority-tagged interface=vlan10_untagged pvid=10
add bridge=bridge1 frame-types=admit-only-untagged-and-priority-tagged interface=vlan20_untagged pvid=20
add bridge=bridge1 frame-types=admit-only-vlan-tagged interface=vlan_tagged
/interface bridge vlan
add bridge=bridge1 tagged=vlan_tagged vlan-ids=10
add bridge=bridge1 tagged=vlan_tagged vlan-ids=20
```

```
[admin@MikroTik] /interface bridge port print
Flags: D - DYNAMIC; H - HW-OFFLOAD
Columns: INTERFACE, BRIDGE, HW, PVID, PRIORITY, HORIZON
#    INTERFACE        BRIDGE   HW   PVID  PRIORITY  HORIZON
0    vlan10_untagged  bridge1  yes    10  0x80      none
1 DH ether2           bridge1  yes    10  0x80      none
2 DH ether3           bridge1  yes    10  0x80      none
3    vlan20_untagged  bridge1  yes    20  0x80      none
4 DH ether4           bridge1  yes    20  0x80      none
5    vlan_tagged      bridge1  yes     1  0x80      none
6 DH sfp-sfpplus1     bridge1  yes     1  0x80      none
```

```
[admin@MikroTik] /interface bridge vlan print
Flags: D - DYNAMIC
Columns: BRIDGE, VLAN-IDS, CURRENT-TAGGED, CURRENT-UNTAGGED
#   BRIDGE   VLAN-IDS  CURRENT-TAGGED  CURRENT-UNTAGGED
;;; added by pvid
0 D bridge1        10                  ether2
                                       ether3
;;; added by pvid
1 D bridge1        20                  ether4
2   bridge1        10  sfp-sfpplus1
3   bridge1        20  sfp-sfpplus1
```

```
# make necessary changes to interface list members:
/interface list member add list=vlan20_untagged interface=ether5
/interface list member add list=vlan_tagged interface=sfp-sfpplus2
```

```
# verify changes in bridge port and vlan menus:
[admin@MikroTik] > /interface bridge port print
Flags: D - DYNAMIC; H - HW-OFFLOAD
Columns: INTERFACE, BRIDGE, HW, PVID, PRIORITY, HORIZON
#    INTERFACE        BRIDGE   HW   PVID  PRIORITY  HORIZON
0    vlan10_untagged  bridge1  yes    10  0x80      none
1 DH ether2           bridge1  yes    10  0x80      none
2 DH ether3           bridge1  yes    10  0x80      none
3    vlan20_untagged  bridge1  yes    20  0x80      none
4 DH ether4           bridge1  yes    20  0x80      none
5 DH ether5           bridge1  yes    20  0x80      none
6    vlan_tagged      bridge1  yes     1  0x80      none
7 DH sfp-sfpplus1     bridge1  yes     1  0x80      none
8 DH sfp-sfpplus2     bridge1  yes     1  0x80      none
```

```
[admin@MikroTik] > /interface bridge vlan print
Flags: D - DYNAMIC
Columns: BRIDGE, VLAN-IDS, CURRENT-TAGGED, CURRENT-UNTAGGED
#   BRIDGE   VLAN-IDS  CURRENT-TAGGED  CURRENT-UNTAGGED
;;; added by pvid
0 D bridge1        10                  ether2
                                       ether3
;;; added by pvid
1 D bridge1        20                  ether4
                                       ether5
2   bridge1        10  sfp-sfpplus1
                       sfp-sfpplus2
3   bridge1        20  sfp-sfpplus1
                       sfp-sfpplus2
```

364
