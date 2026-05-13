## Verify the interface is created: 

```
[admin@AP] > /interface eoip print
Flags: X - disabled; R - running
```

```
 0  R name="eoip-remote" mtu=auto actual-mtu=1458 l2mtu=65535 mac-address=FE:A5:6C:3F:26:C5 arp=enabled
      arp-timeout=auto loop-protect=default loop-protect-status=off loop-protect-send-interval=5s
      loop-protect-disable-time=5m local-address=0.0.0.0 remote-address=10.0.0.2 tunnel-id=0
      keepalive=10s,10 dscp=inherit clamp-tcp-mss=yes dont-fragment=no allow-fast-path=yes
```
