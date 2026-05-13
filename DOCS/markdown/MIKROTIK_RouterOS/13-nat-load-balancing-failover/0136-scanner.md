## Scanner 

It is possible to scan LTE interfaces with `/interface lte scan` command. Example: 

```
[admin@MikroTik] > /interface lte scan duration=60 number=0
Columns: OPERATOR, MCC-MNC, RSSI, RSRP, RSRQ
OPERATOR  MCC-MNC  RSSI    RSRP    RSRQ
LMT         24701  -36dBm  -63dBm  -7dB
```

Available properties: 

**==> picture [209 x 81] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>duration  (integer) Duration of scan in seconds<br>freeze-frame-interval  (integer) time between data printout<br>number  (integer) Interface number or name<br>**----- End of picture text -----**<br>
