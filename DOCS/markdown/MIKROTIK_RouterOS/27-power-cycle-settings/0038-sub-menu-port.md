## Sub-menu: `/port` 

Menu lists all available serial and USB ports on the router and allows to configure port parameters, like baud-rate, flow-control, etc. 

Below you can see default port configuration on LtAP. 

```
[admin@LtAP] > /port/print
Columns: DEVICE, NAME, CHANNELS, USED-BY, BAUD-RATE
# DEVICE  NAME     CHANNELS  USED-BY                                     BAUD-RATE
0         serial0         1  Serial Console(#0)                          auto
1         gps             1  GPS(#0)                                     115200
```

**==> picture [13 x 13] intentionally omitted <==**

List of the ports are maintained automatically by the RouterOS.
