## Packet Template 

```
/tool traffic-generator packet-template
```

This sub-menu allows building packets based on provided parameters. Based on parameters you can build IP packets with VLAN tags and set UDP ports. A raw packet template is generated based on provided parameters. 

If you require more low-level packets or take full advantage of the traffic generator, then please use a raw-packet-template builder to build the packet. 

If the same type of header is present in the packet more than once then header field values are passed as a comma-separated list. (For example, if there are two IP headers then source addresses are given like "IP-src=1.1.1.1,2.2.2.2"). 

For quicker header construction many of the header field values are assumed. For example, if the header stack is "mac, IP" then the traffic generator can assume that the mac-protocol value is "IP". Or if the "port" or "interface" setting is specified traffic generator can assume "mac-src" to be the MAC address of the interface). Assumed values have distinct names that start with "assumed-" and are read-only. Manually specified values override assumed ones. 

**==> picture [13 x 13] intentionally omitted <==**

Assumed values are not automatically updated. New values are assumed after template edit. "packet-template set 0" is enough to trigger new assumed values
