## Monitoring 

To get the active hosts table: 

367 

```
[admin@MikroTik] /interface bridge host print
Flags: X - disabled, I - invalid, D - dynamic, L - local, E - external
 #       MAC-ADDRESS        VID ON-INTERFACE            BRIDGE
 0   D   B8:69:F4:C9:EE:D7      ether1                  bridge1
 1   D   B8:69:F4:C9:EE:D8      ether2                  bridge1
 2   DL  CC:2D:E0:E4:B3:38      bridge1                 bridge1
 3   DL  CC:2D:E0:E4:B3:39      ether2                  bridge1
```
