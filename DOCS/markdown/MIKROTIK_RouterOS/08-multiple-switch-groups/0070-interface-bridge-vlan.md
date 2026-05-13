## `/interface bridge vlan` 

```
add bridge=bridge tagged=bridge untagged=sfp-sfpplus1,sfp-sfpplus2,sfp-sfpplus3,sfp-sfpplus4 vlan-ids=20
add bridge=bridge tagged=bridge untagged=sfp-sfpplus5,sfp-sfpplus6,sfp-sfpplus7,sfp-sfpplus8 vlan-ids=30
```

Routing requires dedicated VLAN interfaces. For standard L2 VLAN bridging (without inter-VLAN routing), the next step can be omitted.
