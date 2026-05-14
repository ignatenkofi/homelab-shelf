## Untagged access with VLAN filtering 

In case VLAN filtering is used and access with untagged traffic is desired, the VLAN interface must use the same VLAN ID as the untagged port VLAN ID ( `pvid` ). Just like in the previous example, start by creating a VLAN interface on the bridge and add an IP address for the VLAN. 

```
/interface vlan
add interface=bridge1 name=MGMT vlan-id=99
/ip address
add address=192.168.99.1/24 interface=MGMT
```

For example, untagged ports ether2 and ether3 should be able to communicate with the VLAN 99 interface using untagged traffic. In order to achieve this, these ports should be configured with the `pvid` that matches the VLAN ID on management VLAN. Note that the bridge1 interface is a tagged port member, you can configure additional tagged ports if necessary (see the previous example). 

```
/interface bridge port
set [find interface=ether2] pvid=99
set [find interface=ether3] pvid=99
/interface bridge vlan
add bridge=bridge1 tagged=bridge1 untagged=ether2,ether3 vlan-ids=99
```

After that you can enable VLAN filtering: 

```
/interface bridge set bridge1 vlan-filtering=yes
```
