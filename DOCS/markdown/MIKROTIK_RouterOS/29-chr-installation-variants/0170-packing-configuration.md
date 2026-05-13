## Packing configuration 

**==> picture [516 x 268] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>aggregated-size (20 .. 16384 default: 1500 ) size of an aggregated packet that packing will try to achieve before sending a packet over the<br>network<br>disabled (yes|no) state of packing rule, if a value is yes it will be ignored and will not be part of the active configuration<br>interface (interface name) packing will try to aggregate and/or compress packets from this interface<br>packing (simple|compress-all|compress- the action it should perform when a packet is leaving the interface packing rule is configured:<br>headers|none)<br>simple  - do just aggregate packets<br>compress-all  - do aggregation and attempt to compress headers and payload of a packet<br>compress-headers  - do aggregation and attempt to compress headers and leave the<br>payload of a packet as is<br>none  - send packets as is<br>unpacking (simple|compress-all|compress- the action should be performed when a packet is received on the interface packing rule is configured<br>headers|none) on:<br>simple  - unpack received packets from aggregated packets received from the interface<br>compress-all  - unpack aggregated packet and uncompress headers and payload of a packet<br>compress-headers  - unpack aggregated packets and decompress headers of a packet<br>none  - do nothing with a received packet<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

The router should be seen as a neighbor of the router over the interface you want to enable packing on. If in the neighbor list there is no entry indicating packing, packing is not working! 

**==> picture [13 x 13] intentionally omitted <==**

Packing may increase latency on the link it is configured on. 

Example 

1906 

Router-A and Router-B are connected with cable with interface ether1 on Router-A and ether3 on Router-B. This example will aggregate packets coming from Router-A, but will leave packets from Router-B intact On Router-A: 

Make sure discovery is enabled: 

```
 /ip neighbor discovery set ether1 discover=yes
```

Add packing rule for the interface: 

- `/ip packing add interface=ether1 aggregated-size=1500 packing=simple unpacking=none` 

On Router-B: 

Make sure discovery is enabled: 

- `/ip neighbor discovery set ether3 discover=yes` 

Add packing rule for the interface: 

```
 /ip packing add interface=ether3 aggregated-size=1500 packing=none unpacking=simple
```

1907
