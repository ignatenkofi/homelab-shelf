## Enable bridge VLAN filtering: 

```
/interface bridge set bridge1 vlan-filtering=yes
```

**==> picture [13 x 13] intentionally omitted <==**

Bidirectional communication is limited only between two switch ports. Translating VLAN ID between more ports can cause traffic flooding or incorrect forwarding between the same VLAN ports. 

**==> picture [13 x 13] intentionally omitted <==**

By enabling `vlan-filtering` you will be filtering out traffic destined to the CPU, before enabling VLAN filtering you should make sure that you set up a Management port.
