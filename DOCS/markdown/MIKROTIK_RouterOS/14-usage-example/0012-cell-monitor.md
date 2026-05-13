## Cell Monitor 

Cell monitor allows to scan available nearby mobile network cells: 

```
[admin@MikroTik] > /interface lte cell-monitor lte1
PHY-CELLID BAND         PSC EARFCN                 RSRP          RSRQ          RSSI         SINR
        49 B20              6300                -110dBm       -19.5dB
       272 B20              6300                -116dBm       -19.5dB
       374 B20              6300                -108dBm         -16dB
       384 B1               150                 -105dBm       -13.5dB
       384 B3               1300                -106dBm         -12dB
       384 B7               2850                -107dBm       -11.5dB
       432 B7               2850                -119dBm       -19.5dB
```

Gathered data can be used for more precise location detection or for Cell lock. 

**==> picture [13 x 13] intentionally omitted <==**

Not all modems support this feature
