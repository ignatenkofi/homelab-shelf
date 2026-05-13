## Interface lists 

Starting with RouterOS v6.41 it possible to add interface lists as a bridge port and sort them. Interface lists are useful for creating simpler firewall rules. Below is an example how to add an interface list to a bridge: 

362 

```
/interface list
add name=LAN1
add name=LAN2
/interface list member
add interface=ether1 list=LAN1
add interface=ether2 list=LAN1
add interface=ether3 list=LAN2
add interface=ether4 list=LAN2
/interface bridge port
add bridge=bridge1 interface=LAN1
add bridge=bridge1 interface=LAN2
```

Ports from an interface list added to a bridge will show up as dynamic ports: 

```
[admin@MikroTik] /interface bridge port> pr
Flags: X - disabled, I - inactive, D - dynamic, H - hw-offload
 #     INTERFACE       BRIDGE       HW  PVID PRIORITY  PATH-COST INTERNAL-PATH-COST    HORIZON
 0     LAN1            bridge1      yes    1     0x80         10                 10       none
 1  D  ether1          bridge1      yes    1     0x80         10                 10       none
 2  D  ether2          bridge1      yes    1     0x80         10                 10       none
 3     LAN2            bridge1      yes    1     0x80         10                 10       none
 4  D  ether3          bridge1      yes    1     0x80         10                 10       none
 5  D  ether4          bridge1      yes    1     0x80         10                 10       none
```

It is also possible to sort the order of lists in which they appear. This can be done using the `move` command. Below is an example of how to sort interface lists: 

```
[admin@MikroTik] > /interface bridge port move 3 0
[admin@MikroTik] > /interface bridge port print
Flags: X - disabled, I - inactive, D - dynamic, H - hw-offload
 #     INTERFACE       BRIDGE       HW  PVID PRIORITY  PATH-COST INTERNAL-PATH-COST    HORIZON
 0     LAN2            bridge1      yes    1     0x80         10                 10       none
 1  D  ether3          bridge1      yes    1     0x80         10                 10       none
 2  D  ether4          bridge1      yes    1     0x80         10                 10       none
 3     LAN1            bridge1      yes    1     0x80         10                 10       none
 4  D  ether1          bridge1      yes    1     0x80         10                 10       none
 5  D  ether2          bridge1      yes    1     0x80         10                 10       none
```

**==> picture [13 x 13] intentionally omitted <==**

The second parameter when moving interface lists is considered as "before id", the second parameter specifies before which interface list should be the selected interface list moved. When moving the first interface list in place of the second interface list, then the command will have no effect since the first list will be moved before the second list, which is the current state either way.
