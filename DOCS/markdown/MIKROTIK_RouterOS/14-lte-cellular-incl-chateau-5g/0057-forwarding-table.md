## Forwarding Table 

Entries in the `/mpls forwarding-table` menu show label bindings for specific routes that will be used in MPLS label switching. Properties in this menu are read-only. 

```
[admin@rack1_b35_CCR1036] /mpls/forwarding-table> print
Flags: L, V - VPLS
Columns: LABEL, VRF, PREFIX, NEXTHOPS
#   LABEL  VRF   PREFIX         NEXTHOPS
0 L    16  main  10.0.0.0/8     { nh=10.155.130.1; interface=ether12 }
1 L    18  main  111.111.111.3  { label=impl-null; nh=111.12.0.1; interface=ether2 }
2 L    17  main  111.111.111.2  { label=impl-null; nh=111.11.0.1; interface=ether1 }
```

**==> picture [496 x 317] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>prefix  (IP/Mask) Destination prefix for which labels are assigned<br>label  (integer) Ingress MPLS label<br>ldp  (yes | no) Whether labels are LDP signaled<br>nexthops  () An array of the next-hops, each entry in the array represents one ECMP next-hop. Array entry can contain several parameters:<br>label  - egress MPLS label<br>nh  - out next-hop IP address<br>interface  - out the interface<br>out-label  (integer) Label number which is added or switched to for outgoing packet.<br>packets  (integer) Number of packets matched by this entry<br>te-sender<br>te-session<br>traffic-eng  Shows whether the entry is signaled by RSVP-TE (Traffic Engineering)<br>type  (string) Type of the entry, for example, "vpls", etc.<br>vpls  (yes | no) Shows whether the entry is used for VPLS tunnels.<br>vpn<br>vrf Name of the VRF table this entry belongs to<br>**----- End of picture text -----**<br>


838 

839
