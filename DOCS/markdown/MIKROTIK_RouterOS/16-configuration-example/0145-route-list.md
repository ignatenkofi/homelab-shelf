## Route list 

RouterOS will show local and received EVPN routes in the `/routing/route` list 

Locally generated routes will hace e-evpn flag. for example: 

```
[admin@ros_leaf_3] /routing/route> print where evpn
Flags: e - EVPN
Columns: DST-ADDRESS, GATEWAY, AFI, DISTANCE, SCOPE, TARGET-SCOPE
  DST-ADDRESS                                     GATEWAY        AFI   DISTANCE  SCOPE  TARGET-SCOPE
e [10.155.101.133:1010]macip:0|0C:50:85:84:00:01  203.0.255.133  evpn       200     40            10
e [10.155.101.133:1010]imet:0|203.0.255.133       203.0.255.133  evpn       200     40            10
e [203.0.255.133:4]imet:0|203.0.255.133           203.0.255.133  evpn       200     40            10
```

EVPN data is encoded in dst-address parameter: 

```
   Dst [rd]type:x|y
```

```
        ^  ^    ^
```

```
        |  |    + - where x - tag or ESI; y - type specific data (can show mac addresses, ip addresses, ethernet
segments etc.)
```

```
        |  +------- name of the EVPN route type (macip, imet, es, ad, prefix)
```

```
        +---------- route distinguisher in square brackets
```
