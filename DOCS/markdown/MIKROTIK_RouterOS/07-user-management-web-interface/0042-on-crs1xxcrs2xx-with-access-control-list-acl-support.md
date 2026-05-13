## On CRS1xx/CRS2xx with Access Control List (ACL) support: 

```
/interface ethernet switch acl
```

```
add action=drop mac-dst-address=01:80:C2:00:00:00 src-ports=ether1
```

In this example all received BPDUs on ether1 are dropped. 

357 

**==> picture [13 x 13] intentionally omitted <==**

If you intend to drop received BPDUs on a port, then make sure to prevent BPDUs from being sent out from the interface that this port is connected to. A root bridge always sends out BPDUs and under normal conditions is waiting for a more superior BPDU (from a bridge with a lower bridge ID), but the bridge must temporarily disable the new root-port when transitioning from a root bridge to a designated bridge. If you have blocked BPDUs only on one side, then a port will flap continuously.
