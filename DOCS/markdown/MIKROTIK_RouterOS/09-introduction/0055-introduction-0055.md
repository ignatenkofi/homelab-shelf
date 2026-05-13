## Introduction 

Many MikroTik devices come with built-in switch chips that usually have an option to do VLAN switching on a hardware level, this means that you can achieve wire-speed performance using VLANs if a proper configuration method is used. The configuration method changes across different models, this guide will focus on setting up a basic trunk/access port with a management port from the trunk port using different devices with the right configuration to achieve the best performance and to fully utilize the available hardware components. 

**==> picture [504 x 237] intentionally omitted <==**

CRS3xx, CRS5xx series switches, CCR2116, CCR2216 and RTL8367, 88E6393X, 88E6191X, 88E6190, MT7621, MT7531 and EN7523 switch chips 

511 

```
/interface bridge
add name=bridge1 frame-types=admit-only-vlan-tagged
/interface bridge port
add bridge=bridge1 interface=ether1 frame-types=admit-only-vlan-tagged
add bridge=bridge1 interface=ether2 pvid=20 frame-types=admit-only-untagged-and-priority-tagged
add bridge=bridge1 interface=ether3 pvid=30 frame-types=admit-only-untagged-and-priority-tagged
/interface bridge vlan
add bridge=bridge1 tagged=ether1 vlan-ids=20
add bridge=bridge1 tagged=ether1 vlan-ids=30
add bridge=bridge1 tagged=ether1,bridge1 vlan-ids=99
/interface vlan
add interface=bridge1 vlan-id=99 name=MGMT
/ip address
add address=192.168.99.1/24 interface=MGMT
/interface bridge
set bridge1 vlan-filtering=yes
```

More detailed examples can be found here. 

**==> picture [13 x 13] intentionally omitted <==**

RTL8367, 88E6393X, 88E6191X, 88E6190, MT7621, MT7531, EN7523 switch chips can use HW offloaded vlan-filtering since RouterOS v7. 

**==> picture [13 x 13] intentionally omitted <==**

Bridge ports with `frame-types` set to `admit-all` or `admit-only-untagged-and-priority-tagged` will be automatically added as untagged ports for the `pvid` VLAN.
