## Torch 

MikroTik Torch is a real-time traffic monitoring tool that can be used to monitor the traffic flow through an interface. Watch our video about this feature. 

**==> picture [13 x 13] intentionally omitted <==**

Traffic that appears in torch is before it has been filtered by a Firewall. This means you will be able to see packets that might get dropped by your Firewall rules. 

```
[admin@MikroTik] > /tool/torch
```

You can monitor traffic classified by: 

source address (IPv4 and IPv6); destination address (IPv4 and IPv6); port; protocol; mac-protocol; VLAN ID; mac-address; DSCP; 

MikroTik Torch shows the protocols you have chosen and the TX/RX data rate for each of them on the particular interface. 

**==> picture [13 x 12] intentionally omitted <==**

Unicast traffic between Wireless clients with client-to-client forwarding enabled will not be visible to the Torch tool. Packets that are processed with hardware offloading enabled bridge will also not be visible (unknown unicast, broadcast and some multicast traffic will be visible to torch tool). 

1820
