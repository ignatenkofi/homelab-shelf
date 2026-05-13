## BFD with BGP 

To enable the use of BFD for BGP sessions, enable `use-bfd` for required entries in `/routing bgp connection` menu. 

A useful feature is that the BGP session will show that the BFD session for that particular BGP session is down: 

```
[admin@dr_02_BGP_MUM] /routing/bgp/session> print
Flags: E - established
 0 E ;;; BFD session down
     name="ovpn_test1-1"
     remote.address=111.111.11.11@vrf1 .as=65530 .id=10.155.101.217
     .capabilities=mp,rr,as4 .hold-time=infinity .messages=40717
     .bytes=3436281 .eor=""
     local.address=111.111.11.12@vrf1 .as=555 .id=111.111.11.12
     .capabilities=mp,rr,gr,as4 .messages=1 .bytes=19 .eor=""
     output.procid=20
     input.procid=20 .filter=bgp-in ebgp
     hold-time=infinity use-bfd=yes uptime=3s210ms
     last-started=2023-05-19 09:54:04 prefix-count=3853
```
