## `/interface bonding` 

```
add name=bonding1 slaves=ether2,ether3,ether4 mode=balance-xor transmit-hash-policy=layer-2-and-3
```

**==> picture [13 x 13] intentionally omitted <==**

You can find a working example for trunking and port-based VLANs on CRS VLANs with Trunks page. 

**==> picture [13 x 13] intentionally omitted <==**

Bridge (R)STP is not aware of the underlying switch trunking configuration and some trunk ports can move to a discarding or blocking state. When trunking member ports are connected to other bridges, you should either disable the (R)STP or filter out any BPDU between trunked devices (e.g. with ACL rules).
