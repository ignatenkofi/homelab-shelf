## Session Menu 

To see the actual active sessions with selected template parameters and negotiated capabilities refer to the BGP sessions menu: 

```
[admin@MikroTik] /routing/bgp/session> print
Flags: E - established
 0 E name="toR2"
     remote.address=192.168.1.2 .as=65532 .id=192.168.1.1 .refused-cap-opt=no
     .capabilities=mp,rr,as4 .afi=ip,ipv6 .messages=43346 .bytes=3635916 .eor=""
     local.address=192.168.1.1 .as=65531 .id=192.168.44.2 .capabilities=mp,rr,gr,as4 .messages=2
     .bytes=71 .eor=""
     output.procid=97 .keep-sent-attributes=no
     .last-notification=ffffffffffffffffffffffffffffffff0015030601
     input.procid=97 .limit-process-routes=500000 ebgp limit-exceeded
     hold-time=3m keepalive-time=1m uptime=4s70ms
```

1012 

This menu shows read-only cached BGP session information. It will show the current status of the session, flags, last received notification, and negotiated session parameters. 

Even if the BGP session is not active anymore, the cache can still be stored for some time. Routes received from a particular session are removed only if the cache expires, this allows mitigating extensive routing table recalculations if the BGP session is flapping.
