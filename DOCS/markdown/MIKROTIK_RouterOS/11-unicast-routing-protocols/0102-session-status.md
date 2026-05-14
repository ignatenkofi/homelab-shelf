## Session Status 

The status of the currently available sessions can be observed from `/routing bfd session` menu: 

```
[admin@dr_02_BGP_MUM] /routing/bfd/session> print
Flags: U - up, I - inactive
 0 I ;;; BFD forbidden for destination address
     multihop=yes remote-address=10.155.101.183 local-address="" desired-tx-interval=0ms required-min-rx=0ms
     multiplier=0
```

```
 1   multihop=no remote-address=111.111.11.11%ovpn-out1@vrf1 local-address=111.111.11.12@vrf1 state=down
     state-changes=0 desired-tx-interval=200ms required-min-rx=200ms remote-min-rx=1us multiplier=5
     packets-rx=0 packets-tx=7674
```

BFD is picking the highest value between the local tx interval and remote minimum rx interval as desired transmit interval. If the session is not established then desired minimum tx interval is set to 1 second. 

1018
