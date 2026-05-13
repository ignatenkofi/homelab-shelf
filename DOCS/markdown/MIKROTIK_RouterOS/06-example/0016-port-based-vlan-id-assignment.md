## Port based VLAN ID assignment 

It is possible to assign an authenticated interface to a specific VLAN ID using bridge VLAN filtering. This can be done using RADIUS Tunnel-Type, Tunnel-Medium-Type and Tunnel-Private-Group-ID attributes. Note that only devices with hardware offloaded VLAN filtering will be able to do this in switch chip. 

287 

First of all, make sure the interface is added to a bridge which has VLAN filtering enabled. 

```
/interface bridge
```

```
add name=bridge1 vlan-filtering=yes
/interface bridge port
add bridge=bridge1 interface=ether1
add bridge=bridge1 interface=ether2
add bridge=bridge1 interface=ether12
```

It is necessary to add static VLAN configuration for tagged VLAN traffic to be sent over ether1 interface. 

```
/interface bridge vlan
add bridge=bridge1 tagged=ether1 vlan-ids=2
add bridge=bridge1 tagged=ether1 vlan-ids=12
```

With enabled RADIUS debug logs it is possible to see complete RADIUS message packets with all attributes. In our example, Tunnel attributes are received in Access-Accept message from RADIUS server: 

```
09:51:45 radius,debug,packet received Access-Accept with id 64 from 10.1.2.3:1812
09:51:45 radius,debug,packet     Tunnel-Type = 13
09:51:45 radius,debug,packet     Tunnel-Medium-Type = 6
09:51:45 radius,debug,packet     Tunnel-Private-Group-ID = "12"
(..)
09:51:45 radius,debug,packet     User-Name = "dot1x-user"
```

The VLAN ID is now present in active session list and untagged ports are added to previously created static VLAN configuration. 

```
/interface dot1x server active print
```

```
 0 interface=ether12 username="dot1x-user" user-mac=00:0C:42:EB:71:F6 session-id="86b00006" vlan=12
```

```
/interface bridge vlan print detail
```

```
Flags: X - disabled, D - dynamic
```

```
 0 D bridge=bridge1 vlan-ids=1 tagged="" untagged="" current-tagged="" current-untagged=bridge1,ether3
```

```
 1   bridge=bridge1 vlan-ids=2 tagged=ether1 untagged="" current-tagged=ether1 current-untagged=ether2
```

```
 2   bridge=bridge1 vlan-ids=12 tagged=ether1 untagged="" current-tagged=ether1 current-untagged=ether12
```
