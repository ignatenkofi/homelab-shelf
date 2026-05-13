## Jumbo frames 

One can increase the total throughput in such a setup by enabling jumbo frames. This reduces the packet overhead by increasing the Maximum Transmission Unit (MTU). If a device in your network does not support jumbo frames, then it will not benefit from a larger MTU. Usually, the whole network does not support jumbo frames, but you can still benefit when sending data between devices that support jumbo frames, including all switches in the path. 

In this case, if clients behind SwitchA and client behind SwitchC support jumbo frames, then enabling jumbo frames will be beneficial. Before enabling jumbo frames, determine the MAX-L2MTU by using this command: 

```
[admin@SwitchA] > interface print
Flags: R - RUNNING
Columns: NAME, TYPE, ACTUAL-MTU, L2MTU, MAX-L2MTU, MAC-ADDRESS
 #   NAME           TYPE   ACTUAL-MTU  L2MTU  MAX-L2MTU  MAC-ADDRESS
 1 R sfp-sfpplus1   ether        1500   1584      10218  64:D1:54:FF:E3:7F
```

**==> picture [13 x 13] intentionally omitted <==**

More information can be found in MTU manual page. 

When MAX-L2MTU is determined, choose the MTU size depending on the traffic on your network, use this command on SwitchA , SwitchB, and SwitchC : 

```
/interface ethernet
set [ find ] l2mtu=10218 mtu=10218
```

578 

Don't forget to change the MTU on your client devices too, otherwise, the above-mentioned settings will not have any effect. 

**==> picture [13 x 13] intentionally omitted <==**

579
