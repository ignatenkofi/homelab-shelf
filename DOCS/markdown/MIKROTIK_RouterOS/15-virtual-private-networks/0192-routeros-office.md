## RouterOS Office 

Configuration on the Office device. We will enable the default instance and ask a controller to join the 879c0b5265a99e4b network: 

```
[admin@office] /zerotier> interface/add network=879c0b5265a99e4b instance=zt1 name=ZT-interface
[admin@office] /zerotier> interface/print interval=1
Columns: NAME, MAC-ADDRESS, NETWORK, STATUS
# NAME          MAC-ADDRESS        NETWORK           STATUS
0 ZT-interface  4A:40:1C:38:97:BA  879c0b5265a99e4b  ACCESS_DENIED
```

As previously, because our network is private, we have to authorize a new peer via "RouterOS home device". After that verify from controller received IP address and route: 

```
[admin@Home] /zerotier> controller/member/print
Flags: A - AUTHORIZED
Columns: NETWORK, ZT-ADDRESS, IP-ADDRESS, LAST-SEEN
#    NETWORK     ZT-ADDRESS  IP-ADDRESS    LAST-SEEN
0 A  ZT-private  879a0b5265  172.27.27.15
1 A  ZT-private  554a914c7f  172.27.27.17
2 A  ZT-private  a83ac6032a  172.27.27.10
3    ZT-private  deba5dc5b1  172.27.27.13  3s348ms
[admin@Home] /zerotier> controller/member/set 3 authorized=yes
[admin@Home] /zerotier> controller/member/print
Flags: A - AUTHORIZED
Columns: NETWORK, ZT-ADDRESS, IP-ADDRESS, LAST-SEEN
#    NETWORK     ZT-ADDRESS  IP-ADDRESS    LAST-SEEN
0 A  ZT-private  879a0b5265  172.27.27.15
```

1290 

```
1 A  ZT-private  554a914c7f  172.27.27.17
2 A  ZT-private  a83ac6032a  172.27.27.10
3 A  ZT-private  deba5dc5b1  172.27.27.13  4s55ms
```

Verify via ZeroTier obtained IP address and route: 

```
[admin@office] /zerotier> /ip/address/print where interface~"ZT"
Flags: D - DYNAMIC
```

```
Columns: ADDRESS, NETWORK, INTERFACE
#   ADDRESS          NETWORK      INTERFACE
0 D 172.27.27.13/24  172.27.27.0  ZT-interface
```

```
[admin@office] /zerotier> /ip/route/print where gateway~"ZT"
Flags: D - DYNAMIC; A - ACTIVE; c, y - COPY
Columns: DST-ADDRESS, GATEWAY, DISTANCE
    DST-ADDRESS     GATEWAY       DISTANCE
DAc 172.27.27.0/24  ZT-interface         0
```
