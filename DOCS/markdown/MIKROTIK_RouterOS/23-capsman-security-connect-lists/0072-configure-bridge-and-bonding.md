## Configure bridge and bonding 

1.  Configure bonding and assign slave interfaces in this setup it is selected as built in wlan1 interface, but it can be also ether interface in other kind of setups. 

For bridge device please set bonding as: 

```
[admin@MikroTik] > /interface bonding add comment=bondingbackup mode=active-backup name=bond1
primary=wlan60-station-1 slaves=wlan60-station-1,wlan1
```

For station-bridge device please set bonding as: 

1441 

```
[admin@MikroTik] > /interface bonding add comment=defconf mode=active-backup name=bond1 primary=wlan60-
1 slaves=wlan60-1,wlan1
```

2. Add interface members (ether1 and bond1) to newly created bridge. 

```
[admin@MikroTik] > /interface bridge port add interface=ether1 bridge=bridge
[admin@MikroTik] > /interface bridge port add interface=bond1  bridge=bridge
[admin@MikroTik] > /interface bridge port print
Flags: X - disabled, I - inactive, D - dynamic, H - hw-offload
 #     INTERFACE                              BRIDGE                              HW   PVID PRIORITY  PATH-
COST    HORIZON
0     ether1                                 bridge                             yes     1     0x80
 1     bond1
bridge                             yes     1     0x80         10                 10       none
```
