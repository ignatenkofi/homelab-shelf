## `/interface bridge vlan` 

```
add bridge=bridge1 tagged=pe1-sfpplus1,sfp-sfpplus2 untagged=pe1-ether1 vlan-ids=10
add bridge=bridge1 tagged=pe1-sfpplus1,sfp-sfpplus2 untagged=pe1-ether2 vlan-ids=20
add bridge=bridge1 tagged=pe1-sfpplus1,sfp-sfpplus2 untagged=pe1-ether3 vlan-ids=30
```

At this point VLANs are configured and devices should be able to communicate through the ports. However, it is recommended to go even a step further and apply some additional filtering options. Enable port `ingress-filtering` on local bridge ports and use frame filtering based on the packet type with `frame-types` setting.
