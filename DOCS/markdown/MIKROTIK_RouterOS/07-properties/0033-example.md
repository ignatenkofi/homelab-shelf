## Example 

To add and enable a bridge interface that will forward L2 packets: 

```
[admin@MikroTik] > interface bridge add
```

```
[admin@MikroTik] > interface bridge print
```

```
Flags: X - disabled, R - running
```

```
0 R name="bridge1" mtu=auto actual-mtu=1500 l2mtu=65535 arp=enabled arp-timeout=auto mac-address=5E:D2:42:95:
56:7F protocol-mode=rstp fast-forward=yes
```

```
igmp-snooping=no auto-mac=yes ageing-time=5m priority=0x8000 max-message-age=20s forward-delay=15s transmit-
hold-count=6 vlan-filtering=no
```

```
dhcp-snooping=no
```
