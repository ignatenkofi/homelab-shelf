## Voltage 

Routers that support voltage monitoring will display supplied voltage value. In CLI/Winbox it will display volts. In scripts/API/SNMP this will be dV or value showed in CLI/Winbox 

Note: Routers that have PEXT and PoE power input are calibrated using PEXT, as a result, value showed over PoE can be lower than input voltage due to additional ethernet protection chains. 

```
[admin@MikroTik] > system/health/print
Columns: NAME, VALUE, TYPE
#  NAME         VALUE  TYPE
0  voltage      23.8   V
1  temperature  39     C
```

**==> picture [13 x 13] intentionally omitted <==**

If old revision CRS112, CRS210 and CRS109 devices are powered with PoE - Health will show correct voltage only up to 26.7V. If higher voltage will be used - Health will show constant 16V. 

1765
