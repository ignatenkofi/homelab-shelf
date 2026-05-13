## Statistics 

Fastpath statistics can be seen from `/openflow/print fast-path` . We can see that in this example fast path is not functional due to complexity of flows Faucet is installing 

```
[admin@CCR2004_2XS_111] /openflow> print fast-path
  openflow-fast-path-packets: 0 0
    openflow-fast-path-bytes: 0 0
```

Port statistics can be seen from `/openflow/port` menu 

```
[admin@CCR2004_2XS_111] /openflow/port> print stats
Columns: INTERFACE, PORT-ID, RX-BYTES, TX-BYTES, RX-PACKETS, TX-PACKETS
# INTERFACE     PORT-ID  RX-BYTES  TX-BYTES  RX-PACKETS  TX-PACKETS
0 sfp-sfpplus1        1    115668     81180        1223        1035
1 sfp-sfpplus2        2    112200     82188        1215        1037
```

944
