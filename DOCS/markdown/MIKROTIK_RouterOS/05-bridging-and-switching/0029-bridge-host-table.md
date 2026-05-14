## Bridge host table 

Bridge host table allows monitoring learned MAC addresses. When `vlan-filtering` is enabled, it shows learned VLAN ID as well (enabled independent-VLAN-learning or IVL). 

```
[admin@MikroTik] > /interface bridge host print where !local
Flags: X - disabled, I - invalid, D - dynamic, L - local, E - external
 #       MAC-ADDRESS        VID ON-INTERFACE       BRIDGE
 0   D   CC:2D:E0:E4:B3:AA  300 ether3             bridge1
 1   D   CC:2D:E0:E4:B3:AB  400 ether4             bridge1
```
