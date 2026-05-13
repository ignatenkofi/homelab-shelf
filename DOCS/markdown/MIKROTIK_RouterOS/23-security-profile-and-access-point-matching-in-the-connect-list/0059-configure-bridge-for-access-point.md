## Configure bridge for Access Point 

1.  Configure bridge for AP to ensure that 5ghz is working as fail-over. It is required to bridge wlan1 , ether1 , and all 60ghz station interfaces . In the example it shows only 2 station devices but it is possible to add up to 8 devices. 

For ap-bridge device please set configuration as follows: 

1438 

```
[admin@MikroTik] >/interface bridge port
add bridge=bridge hw=no interface=ether1
add bridge=bridge interface=wlan1
add bridge=bridge interface=wlan60-station-1
add bridge=bridge interface=wlan60-station-2
[admin@MikroTik] > interface/bridge/port/pr
# INTERFACE         BRIDGE  HW  PVID  PRIORITY  PATH-COST  INTERNAL-PATH-COST  HORIZON
0 ether1            bridge      no     1  0x80             10                  10  none
1 wlan1             bridge             1  0x80             10                  10  none
2 wlan60-station-1  bridge             1  0x80             10                  10  none
3 wlan60-station-2  bridge             1  0x80             10                  10  none
```
