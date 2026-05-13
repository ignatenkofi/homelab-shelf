## Disabled 

If the ARP feature is turned off on the interface, i.e., arp=disabled is used, ARP requests from clients are not answered by the router. Therefore, static ARP entry should be added to the clients as well. For example, the router's IP and MAC addresses should be added: 

```
[admin@host_a] > /ip arp add mac-address=08:00:27:3C:79:3A address=10.155.101.217 interface=ether1
```
