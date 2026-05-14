## `/interface wifi interworking` 

```
add disabled=no domain-names=orion.area120.com hotspot20=yes hotspot20-dgaf=yes internet=yes ipv4-
availability=public ipv6-availability=not-available name=interworking network-type=public-chargeable operator-
names=Orion:eng \
```

```
    realms=orion.area120.com:eap-tls roaming-ois=f4f5e8f5f4,baa2D00100,baa2d00000 venue=business-unspecified
venue-names=Orion:eng wan-downlink=50 wan-status=up wan-uplink=50
```

**==> picture [13 x 13] intentionally omitted <==**

Pay special attention to "wan-downlink" and "wan-uplink", in this scenario value of "50" is used as a placeholder, make sure to adjust the values according to your setup, some client devices use it to evaluate, if they should join the network. Set “venue” – venue type, ”venue-names” and other attributes as applicable. “domain-names” should be of hotspot 2.0 Operator.
