## VRF interfaces in firewall 

**==> picture [13 x 13] intentionally omitted <==**

Before RouterOS version 7.14, firewall filter rules with the property in/out-interface would apply to interfaces within a VRF instance. Starting from RouterOS version 7.14, these rules no longer target individual interfaces within a VRF, but rather the VRF interface as a whole. 

Started from version 7.14 when interfaces are added in VRF - virtual VRF interface is created automatically. If it is needed to match traffic which belongs to VRF interface, VRF virtual interface should be used in firewall filters, for example: 

```
/ip vrf add interfaces=ether5 name=vrf5
/ip firewall filter add chain=input in-interface=vrf5 action=accept
```

If there are several interfaces in one VRF but it is needed to match only one of these interfaces - marks should be used. For example: 

```
/ip vrf add interface=ether15,ether16 vrf=vrf1516
/ip firewall mangle
add action=mark-connection chain=prerouting connection-state=new in-interface=ether15 new-connection-
mark=input_allow passthrough=yes
/ip firewall filter
add action=accept chain=input connection-mark=input_allow
```
