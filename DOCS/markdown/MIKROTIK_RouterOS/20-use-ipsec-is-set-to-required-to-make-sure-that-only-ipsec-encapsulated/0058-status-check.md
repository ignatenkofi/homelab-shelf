## Status Check 

On the LNS you can see all successfully connected clients by checking l2tp server interfaces or checking active ppp connections: 

1242 

```
[admin@CHR_v6_bgp] /interface l2tp-server> print
Flags: X - disabled, D - dynamic, R - running
```

```
# NAME USER MTU CLIENT-ADDRESS UPTIME ENCODING
0 DR <l2tp-... good_worker@mt.lv 1450 10.155.101.216 6h13m49s
```

```
[admin@CHR_v6_bgp] /ppp active> print
Flags: R - radius
# NAME SERVICE CALLER-ID ADDRESS UPTIME ENCODING
0 good_worker@mt.lv l2tp 10.155.101.216 192.168.99.2 6h15m57s
```

On the LAC we can also see active client sessions and active L2TP tunnel between LAC and LNS: 

```
csrLAC#show vpdn
```

```
L2TP Tunnel and Session Information Total tunnels 1 sessions 1
```

```
LocTunID RemTunID Remote Name State Remote Address Sessn L2TP Class/
Count VPDN Group
26090 11 CHR_v6_bgp est 10.155.101.231 50 LAC
```

```
LocID RemID TunID Username, Intf/ State Last Chg Uniq ID
Vcid, Circuit
18521 16 26090 good_worker@mt.lv, Gi1 est 06:17:07 571
```
