## Configuration example 

For two or more devices to be able to connect with each other, they must share the same network-key value. The currently configured network-key can be seen using the monitor command as plc-actual-network-key. 

```
[admin@MikroTik] > /interface pwr-line monitor pwr-line1
name: pwr-line1
connection-to-plc: ok
tx-flow-control: no
rx-flow-control: no
plc-actual-network-key: c973947c200e1540b0f84b571d92bebe
plc-hw-platform: QCA7420
plc-sw-platform: MAC
plc-fw-version: 1.4.0(24-20180515-CS)
plc-line-freq: 50Hz
plc-zero-crossing: detected
plc-mac: B8:69:F4:C4:34:68
```
