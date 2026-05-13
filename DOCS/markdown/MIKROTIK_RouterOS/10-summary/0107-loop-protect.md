## Loop Protect 

The loop protect feature can prevent Layer2 loops by sending loop protect protocol packets and shutting down interfaces in case they receive loop protect packets originating from themselves. The feature works by checking the source MAC address of the received loop-protect packet against the MAC addresses of loop-protect enabled interfaces. If the match is found, loop protect disables the interface that received the loop protect packet. Log message warns about this event and the interface is marked with a loop protect comment by the system. The RouterOS loop protect feature can be used on bridged interfaces as well as on Ethernet interfaces which are set for switching in RouterBoard switch chips. 

Loop Protect works on Ethernet, VLAN, EoIP, VxLAN interfaces and its packets are encapsulated with EtherType 0x9003. 

There the loop protect packet interval and interface disable time can be adjusted. Configuration changes or expiration of disable time, resets loop protection on an interface. 

**==> picture [13 x 13] intentionally omitted <==**

Even though loop-protect can work on interfaces that are added to a bridge, it is still recommended to use (R/M)STP rather than loop-protect since (R/M)STP is compatible with most switches STP variants provide many more configuration options to fine-tune your network.
