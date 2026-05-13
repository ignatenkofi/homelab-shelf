## `/interface bridge port` 

```
set [find where interface=ether1] ingress-filtering=yes frame-types=admit-only-vlan-tagged
set [find where interface=ether2] ingress-filtering=yes frame-types=admit-only-untagged-and-priority-tagged
```

Let's say that you forgot to enable ingress-filtering and change the frame-type property on ether1 , this would unintentionally add access to the device through ether1 using untagged traffic since PVID matches for bridge1 and ether1 , but you are expecting only tagged traffic to be able to access the device. It is possible to drop all untagged packets that are destined for the CPU port :
