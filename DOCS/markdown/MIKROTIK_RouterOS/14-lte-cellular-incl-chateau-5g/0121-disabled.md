## Disabled 

If the ARP feature is turned off on the interface, i.e., `arp=disabled` is used, ARP requests from clients are not answered by the router. Therefore, a static ARP entry should be added to the clients as well. For example, the router's IP and MAC addresses should be added to the Windows workstations using the arp command: 

```
C:\> arp -s 10.5.8.254  00-aa-00-62-c6-09
```
