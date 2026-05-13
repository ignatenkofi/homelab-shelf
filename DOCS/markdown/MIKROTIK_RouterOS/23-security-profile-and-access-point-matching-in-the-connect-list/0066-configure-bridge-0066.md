## Configure bridge 

1.  Add new bridge and assign bridge members to it by issuing the following command: 

```
/interface bridge add name=bridge
```

To check if the bridge has been created issue a command: 

```
[admin@MikroTik] > /interface bridge print
```

```
Flags: X - disabled, R - running
```

```
0 R name="bridge" mtu=auto actual-mtu=1500 l2mtu=65535 arp=enabled arp-timeout=auto mac-address=1A:7F:
BB:41:B0:94 protocol-mode=rstp
```

```
fast-forward=yes igmp-snooping=no auto-mac=yes ageing-time=5m priority=0x8000 max-message-age=20s
forward-delay=15s transmit-hold-count=6
```

```
vlan-filtering=no dhcp-snooping=no
```
