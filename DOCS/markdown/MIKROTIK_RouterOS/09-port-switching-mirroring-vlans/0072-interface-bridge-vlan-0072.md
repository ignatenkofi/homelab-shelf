## `/interface bridge vlan` 

```
add bridge=bridge1 untagged=ether3,ether4,sfp-sfpplus1 vlan-ids=10
add bridge=bridge1 tagged=sfp-sfpplus1 untagged=ether5 vlan-ids=20
```

Last, enable VLAN filtering. Below is the configuration command for Bridge1 and Bridge2: 

```
/interface bridge set [find name=bridge1] vlan-filtering=yes
```

At this point, VLANs and IGMP snooping are configured and devices should be able to communicate through ports. However, it is recommended to go even a step further and apply some additional filtering options. Enable `ingress-filtering` and `frame-types` on bridge ports. Below are the configuration commands for the Bridge1:
