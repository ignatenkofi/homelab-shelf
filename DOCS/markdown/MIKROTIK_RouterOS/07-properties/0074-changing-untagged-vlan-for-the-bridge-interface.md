## Changing untagged VLAN for the bridge interface 

In case VLAN filtering is used, it is possible to change the untagged VLAN ID for the bridge interface using the `pvid` setting. Note that creating routable VLAN interfaces and allowing tagged traffic on the bridge is a more flexible and generally recommended option. 

First, create an IP address on the bridge interface. 

```
/ip address
add address=192.168.99.1/24 interface=bridge1
```

For example, untagged bridge1 traffic should be able to communicate with untagged ether2 and ether3 ports and tagged sfp-sfpplus1 port in VLAN 99. In order to achieve this, bridge1 , ether2 , ether3 should be configured with the same `pvid` and sfp-sfpplus1 added as a tagged member. 

```
/interface bridge
set [find name=bridge1] pvid=99
/interface bridge port
set [find interface=ether2] pvid=99
set [find interface=ether3] pvid=99
/interface bridge vlan
add bridge=bridge1 tagged=sfp-sfpplus1 untagged=bridge1,ether2,ether3 vlan-ids=99
```

After that you can enable VLAN filtering: 

379 

```
/interface bridge set bridge1 vlan-filtering=yes
```

**==> picture [13 x 12] intentionally omitted <==**

If the connection to the router/switch through an IP address is not required, then steps adding an IP address can be skipped since a connection to the router/switch through Layer2 protocols (e.g. MAC-telnet) will be working either way.
