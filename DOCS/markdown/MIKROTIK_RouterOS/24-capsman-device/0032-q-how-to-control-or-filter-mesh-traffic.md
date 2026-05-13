## Q. How to control or filter mesh traffic? 

A. At the moment the only way is to use a bridge firewall. Create a bridge interface, put the WDS interfaces and/or Ethernets in that bridge, and put that bridge in a mesh interface. Then configure bridge firewall rules. 

To match MAC protocol used for mesh traffic encapsulation, use MAC protocol number 0x9AAA, and to match mesh routing traffic, use MAC protocol number 0x9AAB. Example: 

```
interface bridge settings set use-ip-firewall=yes
interface bridge filter add chain=input action=log mac-protocol=0x9aaa
interface bridge filter add chain=input action=log mac-protocol=0x9aab
```

**==> picture [13 x 13] intentionally omitted <==**

It is perfectly possible to create mixed mesh/bridge setups that will not work (e.g. Problematic example 1 with bridge instead of a switch). The recommended fail-safe way that will always work is to create a separate bridge interface per each of the physical interfaces; then add all these bridge interfaces as mesh ports.
