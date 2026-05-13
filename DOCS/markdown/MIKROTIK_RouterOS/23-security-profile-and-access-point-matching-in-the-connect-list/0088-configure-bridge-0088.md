## Configure bridge 

1.  Add new bridge and assign bridge members to it by issuing the following command: 

```
/interface bridge add name=bridge
```

To check if the bridge has been created issue a command: 

```
[admin@MikroTik] > /interface bridge print
Flags: X - disabled, R - running
0 R name="bridge" mtu=auto actual-mtu=1500 l2mtu=65535 arp=enabled arp-timeout=auto mac-address=1A:7F:
BB:41:B0:94 protocol-mode=rstp
fast-forward=yes igmp-snooping=no auto-mac=yes ageing-time=5m priority=0x8000 max-message-age=20s
forward-delay=15s transmit-hold-count=6
vlan-filtering=no dhcp-snooping=no
```

2.  Add interface members (ether1 and wlan60-1) to newly created bridge. 

```
[admin@MikroTik] > /interface bridge port add interface=ether1 bridge=bridge
[admin@MikroTik] > /interface bridge port add interface=wlan60-1 bridge=bridge
[admin@MikroTik] > /interface bridge port print
Flags: X - disabled, I - inactive, D - dynamic, H - hw-offload
 #     INTERFACE                              BRIDGE                              HW   PVID PRIORITY  PATH-
COST    HORIZON
0     ether1                                 bridge                             yes     1     0x80
 1 I   wlan60-
1                               bridge                                     1     0x80         10
```
