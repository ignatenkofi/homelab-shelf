## Align 

```
/interface w60g align wlan60-1
connected: yes
frequency: 58320
remote-address: 04:D6:AA:AA:AA:AB
tx-mcs: 6
tx-phy-rate: 1540.0Mbps
signal: 70
rssi: -62
10s-average-rssi: -63.1
tx-sector: 62
tx-sector-info: left 19 degrees, up 26.6 degrees
rx-sector: 96
distance: 220.88m
tx-packet-error-rate: 5%
```

In align mode frames between two devices are exchanged more rapidly and information about signal quality is displayed more often. Use "rssi", "10saverage-rssi" and "tx-sector-info" (available from 6.44beta39) values for more precise link alignment. When devices enter align mode - link is lost for a few seconds.
