## Devices 

In this menu you can check and set general Bluetooth chip parameters: 

```
/iot bluetooth print
Columns: NAME, PUBLIC-ADDRESS, RANDOM-STATIC-ADDRESS, ANTENNA
  #  NAM  PUBLIC-ADDRESS     RANDOM-STATIC-ADD  ANTENNA
  0  bt1  00:00:00:00:00:00  F4:4E:E8:04:77:3A  internal
/iot bluetooth set
```

note : Public address is the IEEE registered, permanent address. This address can not be changed. In the "print" example above, the device does not have a public address assigned (all octets are set to 0). 

Configurable settings are shown below: 

**==> picture [402 x 81] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>antenna  (string; Default: internal) Choose whether to use an internal or an external Bluetooth antenna<br>name  (string; Default: ) Descriptive name of Bluetooth chip/interface<br>random-static-address  (MAC address; Default: ) A user-configurable address for the Bluetooth chip<br>**----- End of picture text -----**<br>

You can monitor chip stats with the command: 

```
/iot bluetooth print stats
```

```
Columns: NAME, RX-BYTES, TX-BYTES, RX-ERRORS, TX-ERRORS, RX-EVT, TX-CMD, RX-ACL, TX-ACL
  #  NAM  RX-BYTE  TX-  R  T  RX-EV  TX  R  T
  0  bt1  1857835  235  0  0  46677  45  0  0
```
