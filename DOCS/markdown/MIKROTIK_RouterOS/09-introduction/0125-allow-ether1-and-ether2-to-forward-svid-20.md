## Allow ether1 and ether2 to forward SVID 20: 

```
/interface ethernet switch vlan
add ports=ether1,ether2 vlan-id=20
```

Override the SVID EtherType (0x88a8) to CVID EtherType (0x8100) on ether2 : 

```
/interface ethernet switch port
```

```
set ether2 egress-service-tpid-override=0x8100 ingress-service-tpid-override=0x8100
```

562 

Enable unknown/invalid VLAN filtering: 

```
/interface ethernet switch
```

```
set drop-if-invalid-or-src-port-not-member-of-vlan-on-ports=ether1,ether2
```

**==> picture [13 x 13] intentionally omitted <==**

Since the switch is set to look up VLAN ID based on the service tag, which is overridden with a different EtherType, then VLAN filtering is only done on the outer tag of a packet, the inner tag is not checked.
