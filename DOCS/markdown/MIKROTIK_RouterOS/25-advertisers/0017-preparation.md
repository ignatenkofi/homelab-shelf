## Preparation 

Before we proceed, we need to confirm that our Bluetooth tag actually appears in the KNOT's Bluetooth range and that the KNOT detects them. To do that, you can issue the command " `/iot bluetooth scanners advertisements print` ": 

```
/iot bluetooth scanners advertisements print
 # DEVICE     PDU-TYPE        TIME                 ADDRESS-TYPE ADDRESS                    RSSI     LENGTH
DATA
 0 bt1        adv-noconn-ind  mar/08/2023 12:35:15 public       2C:C8:1B:4B:BB:0A        -50dBm         22
15ff4f090100b0110100ffff00000019d68d2300005d
 1 bt1        adv-noconn-ind  mar/08/2023 12:35:16 public       DC:2C:6E:0F:C0:3D        -39dBm         22
15ff4f0901008f3cfcfffbfffaff301783c22c000064
 2 bt1        adv-noconn-ind  mar/08/2023 12:35:35 public       2C:C8:1B:4B:BB:0A        -50dBm         22
15ff4f09010084d500000400ffff0319ea8d2300005d
 3 bt1        adv-noconn-ind  mar/08/2023 12:35:45 public       2C:C8:1B:4B:BB:0A        -50dBm         22
15ff4f090100e607faffffff03000319f48d2300005d
```

Or you can check it using Webfig or Winbox under the IoT>Bluetooth>Advertising reports tab. 

The list can be chaotic. Random payloads can appear on the list as the scanner captures everything around it. To help reduce the list, you can filter it using the tag's MAC address " `/iot bluetooth scanners advertisements print where address=DC:2C:6E:0F:C0:3D` ": 

```
/iot bluetooth scanners advertisements print where address=DC:2C:6E:0F:C0:3D
 # DEVICE    PDU-TYPE        TIME                 ADDRESS-TYPE ADDRESS                    RSSI     LENGTH
DATA
 0 bt1       adv-noconn-ind  mar/08/2023 12:41:06 public       DC:2C:6E:0F:C0:3D        -49dBm         22
15ff4f0901005ab20100fdfffdff4017e1c32c000064
 1 bt1       adv-noconn-ind  mar/08/2023 12:41:26 public       DC:2C:6E:0F:C0:3D        -40dBm         22
15ff4f090100349704000000fcff4017f5c32c000064
 2 bt1       adv-noconn-ind  mar/08/2023 12:41:36 public       DC:2C:6E:0F:C0:3D        -49dBm         22
15ff4f09010073fb0000000000003017ffc32c000064
 3 bt1       adv-noconn-ind  mar/08/2023 12:41:46 public       DC:2C:6E:0F:C0:3D        -43dBm         22
15ff4f090100b88cffffffffffff401709c42c000064
```

To figure out how to decypher the payload, please check the guide here.
