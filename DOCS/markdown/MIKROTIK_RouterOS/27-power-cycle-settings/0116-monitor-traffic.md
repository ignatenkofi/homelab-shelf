## Monitor traffic 

The traffic passing through any interface can be monitored using the `monitor-traffic` command. 

1768 

```
[admin@MikroTik] > /interface monitor-traffic [find]
                         name:     ether1 ether2 ether3 ether4 ether5 sfp1
        rx-packets-per-second:         19      0      0      0      0    0
           rx-bits-per-second:   27.8kbps   0bps   0bps   0bps   0bps 0bps
     fp-rx-packets-per-second:         29      0      0      0      0    0
        fp-rx-bits-per-second:   26.8kbps   0bps   0bps   0bps   0bps 0bps
        tx-packets-per-second:         21      0      0      0      0    0
           tx-bits-per-second:  149.4kbps   0bps   0bps   0bps   0bps 0bps
     fp-tx-packets-per-second:          0      0      0      0      0    0
        fp-tx-bits-per-second:       0bps   0bps   0bps   0bps   0bps 0bps
    tx-queue-drops-per-second:          0      0      0      0      0    0
```

**==> picture [13 x 13] intentionally omitted <==**

Additional Ethernet statistics are available in the "/interface ethernet" menu. 

1769
