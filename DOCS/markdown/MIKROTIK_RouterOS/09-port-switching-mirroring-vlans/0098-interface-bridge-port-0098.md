## `/interface bridge port` 

```
set [find interface=pe1-ether1] frame-types=admit-only-untagged-and-priority-tagged
set [find interface=pe1-ether2] frame-types=admit-only-untagged-and-priority-tagged
set [find interface=pe1-ether3] frame-types=admit-only-untagged-and-priority-tagged
set [find interface=pe1-sfpplus1] frame-types=admit-only-vlan-tagged
set [find interface=sfp-sfpplus2] frame-types=admit-only-vlan-tagged ingress-filtering=yes
```

**==> picture [13 x 13] intentionally omitted <==**

Port ingress VLAN filtering is not supported on extended ports.
