## `/interface vlan` 

```
add interface=ether1 name=VLAN_ether1 vlan-id=999
add interface=ether2 name=VLAN_ether2 vlan-id=999
/interface bonding
```

```
add mode=balance-xor name=bond1 slaves=VLAN_ether1,VLAN_ether2 transmit-hash-policy=layer-2-and-3
/ip address
add address=192.168.1.X/24 interface=bond1
add address=192.168.11.X/24 interface=ether1
add address=192.168.22.X/24 interface=ether2
```

AP1 and ST1 only need updated IP addresses to the correct subnet: 

```
/ip address
```

```
add address=192.168.11.X/24 interface=bridge1
```

598 

Same changes must be applied to AP2 and ST2 (make sure to use the correct subnet): 

```
/ip address
```

```
add address=192.168.22.X/24 interface=bridge1
```

With this approach, you create the least overhead and the least configuration changes are required. 

**==> picture [13 x 13] intentionally omitted <==**

LACP (802.3ad) is not mean to be used in setups, where devices bonding slaves are not directly connected, in this case, it is not recommended to use LACP if there are Wireless links between both routers. LACP requires both bonding slaves to be at the same link speeds, Wireless links can change their rates at any time, which will decrease overall performance and stability. Other bonding modes should be used instead.
